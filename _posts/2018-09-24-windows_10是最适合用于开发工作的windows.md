---
published: true
---
windows XP之后就基本没有用过windows了，一直都是mac加ubuntu加centos。windows只有在需要写公司标准幻灯片或者使用国内网银时候用。感觉用windows开发很麻烦，java，maven，git，python都得安装配置一遍，自己的一些alias命令和vim配置也用不了。

公司刚刚升级了windows 10的电脑，打开觉得很新奇，界面好看了很多，偶然发现windows store里有ubuntu这个app。

刚开始以为是docker image，后来google了下，他是windows subsystem for linux(WSL), 目前只有ubuntu只一种distro。有些程序员也管它叫windows bash。 秒级启动，目前没有发现兼容性问题，在WSL里启动的apache在windows里直接访问，完全不用配置。

我现在用ConEum + WSL bash. 再简单把ConEum配成Guake式，F10呼出，占据上半个屏幕。下图是ConEum的官网截图。

![]({{site.baseurl}}/https://conemu.github.io/img/ConEmu-Maximus5.png)

好像还有一种ComEum + WSL bash + MobaXterm的做法，可以启动X11, 我也不需要X11，所以没有去做太多的了解。

这样的话，我完全就可以用windows来作为开发机器了，还能用office套件，linux上的Thunerbird和pidgin难用到令人发指。如果没有什么兼容性问题的话，我会继续在开发机器上使用windows 10。



======================== 09-25 更新
WSL的Ubuntu 14.04以后的版本上apache有些问题。我在Apache 2上配了一个wsgi跑django。结果一访问就cpu飙升到顶。stackoverflow上也有哥们遇到了同样的问题 - 

[overload-server-django-deploy-with-apache2-and-mod-wsgi](https://stackoverflow.com/questions/51036939/overload-server-django-deploy-with-apache2-and-mod-wsgi)
