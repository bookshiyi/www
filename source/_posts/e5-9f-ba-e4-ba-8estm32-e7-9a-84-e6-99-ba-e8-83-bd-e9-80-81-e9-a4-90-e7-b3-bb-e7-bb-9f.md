---
title: 基于STM32的智能送餐系统
tags:
  - HMI
  - SIM900A
  - STM32
  - UART
  - 智能送餐柜
  - 结构体
  - 迪文
  - 验证码
url: 926.html
id: 926
comments: false
categories:
  - STM32
  - 单片机
  - 嵌入式
  - 硬件设计
  - 软件设计
date: 2016-06-13 10:53:54
---

Github地址：[http://github.com/oarap-org/smartbox_stm32](http://github.com/oarap-org/smartbox_stm32)

硬件原理图：[smartbox rev1.4](https://assets.bookshiyi.com/file/2016/06/smartbox-rev1.4.pdf)   （已经在中国矿业大学组装完成进行样机测试）

        随着送餐平台不断发展，校园送餐的一些细节矛盾显现出来，其中之一便是送餐效率问题，学校出于安全的考虑，导致送餐员无法送餐达寝室，只能在楼下给订餐同学打电话通知然后等待，而顾客也要放下手头的工作下楼，这样极大的降低了送餐的效率，本系统的设计旨在解决送餐员与顾客之间的等待问题，彻底解决送餐过程中的“最后50米”，提高送餐员的工作效率的同时也让给订餐同学任意安排取餐时间的自由。系统的设计理念以便捷、高效为主，专注于提高送餐的效率。

#### 展示视频：

或

### **[点我观看视频](http://v.youku.com/v_show/id_XMTYxODAxMjI2NA==.html)**

 

###         1.系统的工作流程

        送餐员在扫描过外卖上的条形码后会根据当前的订单号开启一个餐柜，同时用户会收到一条还有随机验证码的短信，用户在取餐界面输入随机验证码后会打开相对应的餐柜，外卖被取走后订单完成。

![smartbox_work_flow_chart](https://assets.bookshiyi.com/photo/2016/06/smartbox_work_flow_chart.png)

###  2.硬件框图

![smartbox_struct_chart](https://assets.bookshiyi.com/photo/2016/06/smartbox_struct_chart.png)

###         3.系统原理图

![smartbox_sch](https://assets.bookshiyi.com/photo/2016/06/smartbox_sch.png)

###         4.软件流程图

![smartbox_software_flow_chart](https://assets.bookshiyi.com/photo/2016/06/smartbox_software_flow_chart.png)

###         5.内部自建数据库

![smartbox_database_chart](https://assets.bookshiyi.com/photo/2016/06/smartbox_database_chart.png)

###         6.样机图片

![](https://assets.bookshiyi.com/photo/2016/06/smartbox_kuangda_1.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_kuangda_2.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_kuangda_3.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_kuangda_4.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_kuangda_5.jpg)

* * *

![](https://assets.bookshiyi.com/photo/2016/06/smartbox_1.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_2.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_3.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_4.jpg) ![](https://assets.bookshiyi.com/photo/2016/06/smartbox_5.jpg)

* * *