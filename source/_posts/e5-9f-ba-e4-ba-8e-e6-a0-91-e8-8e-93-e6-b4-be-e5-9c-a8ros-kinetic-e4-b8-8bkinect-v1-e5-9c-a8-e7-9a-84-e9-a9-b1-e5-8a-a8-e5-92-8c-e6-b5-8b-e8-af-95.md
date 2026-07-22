---
title: 基于树莓派在ROS Kinetic下Kinect V1在的驱动和测试
tags:
  - freenect
  - kinect
  - RGB-D
  - ROS
  - slam
  - Ubuntu
  - 树莓派
  - 深度传感器
url: 1571.html
id: 1571
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 开源
  - 开源硬件
  - 开源软件
  - 机器人
  - 树莓派
  - 深度传感器
date: 2017-03-28 17:59:43
---

#### 开发环境：**树莓派3B** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **Kinect V1**

       大部分的教程会提示你安装openni驱动Kinect，但实际上这并不一定能让你的Kinect传感器工作，本文将介绍基于freenect驱动Kinect v1的方法。

0x00 开始前请确保你的Kinect v1通过USB2.0与ROS计算机相连接，并且Kinect v1的电源功率足够；

$ sudo apt-get install  ros-kinetic-freenect-*
$ rospack profile

        0x01：启动你的freenect节点(确保你的roscore已经在运行)：

rosrun freenect\_camera freenect\_node

         0x02：使用rqt\_image\_view工具预览Kinect的画面（也可以使用rqt\_rviz或者rqt\_gui工具）：

rosrun rqt\_image\_view rqt\_image\_view

         0x03：选择深度或RGB话题以显示画面

![](https://assets.bookshiyi.com/photo/2017/03/kinect_freenect_depth_view.jpg) ![](https://assets.bookshiyi.com/photo/2017/03/kinect_freenect_rgb_view.jpg)

ps：3D点云形式的查看

roslaunch freenect_launch freenect.launch

* * *