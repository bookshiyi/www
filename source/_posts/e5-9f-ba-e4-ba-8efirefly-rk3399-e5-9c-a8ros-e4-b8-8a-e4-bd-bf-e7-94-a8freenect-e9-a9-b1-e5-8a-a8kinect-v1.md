---
title: 基于Firefly-RK3399在ROS上使用freenect驱动Kinect v1
tags:
  - freenect
  - kinect
  - openni
  - rgbd
  - rk3399
  - ROS
url: 1637.html
id: 1637
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 只文本模式
  - 开源
  - 开源硬件
  - 开源软件
  - 机器人
  - 深度传感器
date: 2017-04-05 09:20:50
---

#### 开发环境：**Firefly-RK3399** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **Kinect V1**

0x00 开始前请确保你的Kinect v1通过USB2.0与ROS计算机相连接，并且Kinect v1的电源功率足够；

        0x01 安装**freenect**驱动**：**

$sudo apt-get install ros--freenect-*
$rosstack profile
$rospack profile 

        0x02 运行**lsusb**后能看到三个设备：

![](https://assets.bookshiyi.com/photo/2017/04/kinect_lsusb.jpg)

        0x03 运行**freenect**节点

$rosrun freenect\_camera freenect\_node

* * *

        **问题出现**：尽管freenect对与kinect的支持非常好，但是由于多平台的差异性，也有可能出现这样的错误：

##### **        No devices connected... Waiting for devices to be connected**

        请尝试如下解决方案：

        0x04 安装**openni_pack** 和**openni_stack：**

$sudo aptget install ros--openni-camera ros--openni-launch
$rosstack profile 
$rospack profile 

        0x05 再次运行**freenect**节点

$rosrun freenect\_camera freenect\_node

        问题解决

  
  
  

* * *

        最后感谢FireFly团队提供的**RK3399**高性能、奢侈配置的开发板(点击图片了解详情)：

[![](https://assets.bookshiyi.com/photo/2017/04/firefly_rk3399_preview.png)](http://www.t-firefly.com/zh/firenow/Firefly-rk3399/)

* * *