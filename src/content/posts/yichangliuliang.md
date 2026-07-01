---
title: 异常流量
published: 2026-06-25
description: 最近在更新短链站点时，通过短链新更新的网站可用性检测时发现之前搭建的github反代站404了
image: https://img.jiu521.pp.ua/file/share/anime/1782284449045.png
tags:
  - edgeone
  - 反代
category: 运维笔记
draft: false
lang: zh-CN
---
# 请求数异常

最近在将sink更新到最新版本测试新功能时，新版本有个检测短链链接的功能，发现之前创建的短链出现了404，一看网址，是之前部署在edgeone的github反代

还在想怎么回事，于是打开edgeone的控制台一看
![屏幕截图_25-6-2026_03317_console.tencentcloud.com.jpeg](https://img.jiu521.pp.ua/file/Uploads/1782372970569.jpeg)

好嘛，近**7天505.9w**次，总流量**30.51GB**。

![a16336f474e8b6edaa3c026932124f67.png](https://img.jiu521.pp.ua/file/Uploads/1782373228263.png)

从2026-06-17开始总共请求了有**603.97w**次，发生了什么？？？

这个站点就我一个人用，哪来这么多请求，而且非常规律，每5分钟3k次

一看统计

![dc490152917a640493d4331eadb5a256.png](https://img.jiu521.pp.ua/file/Uploads/1782373343977.png)

bot？？？

![dee484ad000d54e661a78edfc395259d.png](https://img.jiu521.pp.ua/file/Uploads/1782373434978.png)

**claudebot？？？**

什么叫做claudbot每5分钟访问我的域名3k次？？？什么叫每天86w次请求？？？什么叫做每天**4.74GB**流量在404页？？？

打开AI爬虫处理后又拦截了4865次，然后请求就恢复正常了

![image.png](https://img.jiu521.pp.ua/file/Uploads/1782374007285.png)
![image.png](https://img.jiu521.pp.ua/file/Uploads/1782374178863.png)

# 网页的404还是没有解决

我看了一眼账户消息，2026-06-17 pages功能正式上线，和我反代站请求异常刚好对上，不知道有没有关系

我检查了一下发现直接访问域名就直接404，访问预览链接也是404

我去看了下官方频道有没有解决办法，但没找到，这个网站的源码我也忘记是哪个了

![image.png](https://img.jiu521.pp.ua/file/Uploads/1782375469765.png)

检查了一下构建历史没有问题，于是直接回退版本

最后反代站能正常工作了