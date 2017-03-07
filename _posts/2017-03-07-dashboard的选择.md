---
published: true
---
搞DevOps难免需要弄个dashboard出来放在大屏幕上上显示各种东西.KPI啊,产品build pipeline啊,服务器负载啊,测试通过率等等.看了些dashboard应用.在这记录一下.

1. [geckoboard](https://www.geckoboard.com/)

颜色搭配看着舒服,扁平化也做得酷炫.他们相当于是做SaaS的,客户不需要自己安装部署他们的dashboard产品,直接用他们给的现成的就好.价钱不算便宜,支持5个dashboard的plan就是149美元一个月,支持一个dashboard的要25美元一个月.
![geckboard.png]({{site.baseurl}}/images/geckboard.png)

2. [freeboard](https://freeboard.io/)

有0美元一个月的,也有最贵100美元一个月的plan.开源,[repo在这](https://github.com/Freeboard/freeboard). github的项目介绍说 -
> A damn-sexy, open source real-time dashboard builder for IOT and other web mashups. A free open-source alternative to Geckoboard.
damn-sexy....听起来就像几个能量饮料喝太多的美国宅男在车库里搞出来的东西.五颗星推荐!
![freeboard.png]({{site.baseurl}}/images/freeboard.png)

3. [appinsights](https://www.appinsights.com/)

一般,最便宜的都要89美元一个月.界面没有~~impresive~~令人印象深刻. 你有没有发现,这些dashboard全是黑灰色的.这是目前的web潮流色吗? 
![appinsight.png]({{site.baseurl}}/images/appinsight.png)

4. [dashing](http://dashing.io/)

业界良心!开源免费!虽然官方已经停止维护一段时间了,但是没有大的bug.第三方widget也很丰富.他们的[github wiki](https://github.com/Shopify/dashing/wiki/Additional-Widgets)上列了大概两三百个widget.小弟我也做了一个[google line chart widget](https://gist.github.com/lizer/bfb71771537e437618c8),能在dashboard上使用google的线图.
![dashing.png]({{site.baseurl}}/images/dashing.png)

现在我身后的大屏幕上就滚动播放着几个dashboard.这些dashboard显示着我们云端测试环境池的信息,知道怎么读图以后瞟一眼就知道个池子情况的大概,如下图.dashing有被动和主动两种刷新方式.被动就是dashing接收rest interface传来数据.主动就是用"job"ruby脚本来主动收集数据.
![my_dashing.png]({{site.baseurl}}/images/my_dashing.png)

5. [cyfe](https://www.cyfe.com/)

又双叒叕是一个黑灰色的dashboard.有免费服务,收费服务也不贵,不到20美元.很多公司在用所以产品质量和支持应该都不错.
![cyfe.png]({{site.baseurl}}/images/cyfe.png)

6. [klipfolio](https://www.klipfolio.com/features)

把这个放在最后介绍没有任何目的,纯粹是在最后看到了这个dashboard产品.非常失望,又双叒叕又双叒叕又双叒叕是一个默认黑灰色的背景
![klipfolio.png]({{site.baseurl}}/images/klipfolio.png)



##写在最后
1. 实在没有精力去写一个各个dashboard产品横向对比.总而言之,不想付钱的话,考虑dashing和freeboard.不差钱的话就geckoboard.
2. wordpress在dashboard界真流行...除了dashing的官网,其他五个都是wordpress做的或者是wordpress风..
