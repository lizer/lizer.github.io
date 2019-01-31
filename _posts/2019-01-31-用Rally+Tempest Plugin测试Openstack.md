---
published: false
---
## 背景
部门装了10几套openstack了，每套32或64台满配的HP gen9 blade server。Openstack是用的是红帽的，差不多2年前开始安装第一套。当初还是做Prove Of Concept（POC）为主，试试我们的产品的openstack上运行得怎么样，红帽的客户支持好不好。Day 2 operations比如故障监测，自动CI没有考虑太多，当时就是先把我们的产品在我们自己的openstack上跑起来再说。后来openstack部署得越来越多，管理起来很困难，尤其是Life Cycle Mgmt，让人痛苦不堪，以至于索性放弃了patch，只做major release的升级。即便是这样，还是有大量的人力投入在LCM上，今年又计划了3套新的openstack，借着这个机会，我们决定顺便把CI先做了，在新的这几套openstack上试试水。

## 先安装一套all-in-one concept cloud
用RDO的Packstack就能一键式安装all-in-one concept cloud，需要一台centos的服务器，最少16GB内存，core最好两个以上。我用了一台vm。

第一步 - 安装packstack

第二步 - 用packstack安装all-in-one concept cloud (all-in-one concept cloud 安装可以不需要answerfile，用默认的packstack--allinone命令安装就行，除非有特殊的需求)

（第一步和第二步具体的步骤可以参考 https://www.rdoproject.org/install/packstack/）

## 安装Rally+Openstack plugin
我把Rally装到了另一台vm上。
Rally安装文档 - https://rally.readthedocs.io/en/latest/quick_start/tutorial/step_0_installation.html
注意两点！
第一点 - Rally和Tempest插件会有很多依赖的版本和本地环境有冲突，所以最好用非root用户新建一个virtual env来保存rally的依赖Rally已经把这个部分cover了，在安装文档里有详细说明，用户只需要直接运行安装脚本就好，如果是非root用户，rally会自动创建一个新的virtual env。

If you execute the script as regular user, Rally will create a new virtual environment in ~/rally/ and install in it Rally, and will use sqlite as database backend. If you execute the script as root, Rally will be installed system wide. For more installation options, please refer to the installation page.



第二点 - Rally没有默认安装openstack plugin。你需要用pip install rally-openstack来安装。出现冲突的话用pip install pkg-name==version来解决，例如pip install openstack-novaclient==10.2.1。

用#rally plugin list --platform openstack验证openstack plugin是否安装成功。
如果有类似下面的Warning的话就把依赖冲突问题先fix。（用#pip install pkg-name==version）
2019-01-30 11:58:46.168 25869 WARNING rally.common.plugin.discover [-]   Failed to load plugins from module 'rally_openstack' (package: 'rally-openstack 1.3.0'): (python-novaclient 7.1.2 (/usr/lib/python2.7/site-packages), Requirement.parse('python-novaclient>=9.1.0')): VersionConflict: (python-novaclient 7.1.2 (/usr/lib/python2.7/site-packages), Requirement.parse('python-novaclient>=9.1.0'))
Plugin existing not found

## 安装Tempest plugin
同样的Rally也能自动安装。运行下面的命令新建一个Tempest verifier，Rally会自动安装Tempest
#rally verify create-verifier --type tempest --name tempest-verifier
详细介绍见下链接 - 
https://rally.readthedocs.io/en/latest/quick_start/tutorial/step_9_verifying_cloud_via_tempest_verifier.html

## 同步一个project到Rally
第一步 - 把admin的credential文件copy到Rally的server上。然后source一个这个credentials文件。（在virtual env里source是ok的，两者里的环境变量会叠加）。


第二步 - 把admin project的信息同步到Rally。我用了--fromenv，还有其他选项，比如--filename，这个file好像不能是openstack的credential文件，而需要时一个json格式的文件。我试了下credential文件，结果报错了。--name是这个project在Rally里的名字，可以不用和project在openstack里一致。
#rally deployment create --fromenv --name admin

## 触发Tempest测试
#rally verify start --deployment-id admin --id tempest-verifier
测试跑了7个小时，一共1558个测试过了1097。可能因为是测试环境配置和负载能力有限，很多testcase失败是timeout了，这也造成了测试过程总体耗时比较久。

测试结束后，可以生成html报告。
#rally verify report --uuid ed1ed4e2-c003-4339-a761-413334bfaed1 --type html --to report.html


测试过程中我观察了几分钟openstack上的系统开销。nova-conductor, httpd, qemu-kvm, neutron-server等都飙到70%以上的CPU用量。不是到在实际的production openstack里，跑Tempest测试会不会影响到openstack的性能。等后面有时间再验证了。


