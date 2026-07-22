---
title: 基于Firefly-RK3399使用Kinect v1通过freenect和depthimage_to_laserscan得到伪激光数据
tags:
  - fake_laser
  - freenect
  - kinect
  - lasersacn
  - ROS
url: 1669.html
id: 1669
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 只文本模式
  - 同步定位与建图
  - 开源
  - 开源硬件
  - 开源软件
  - 机器人
  - 深度传感器
date: 2017-04-05 15:48:23
---

####         开发环境：**Firefly-RK3399** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **Kinect V1**

        0x00 开始前请确保你的Kinect v1通过USB2.0与ROS计算机相连接，并且Kinect v1的电源功率足够；

        0x01 确保已经安装**freenect**（如果没安装请移步[freenect安装教程](https://assets.bookshiyi.com/archives/1571)）；

        0x02 安装**depthimage\_to\_laserscan：**

方式一：源码安装

    cd ~/catkin_ws/src  
    git clone --branch indigo-devel https://github.com/ros-perception/depthimage\_to\_laserscan.git  
    cd ..  
    catkin_make  

方式二：功能包安装(推荐)

    sudo apt-get install ros--depthimage-to-laserscan 

        0x03 在ROS By Example 1一书中（90页）给出了基于openni的伪激光launch，本文将给出基于freenect和depthimage\_to\_laserscan的fake_laser.launch代码：

` 

        第4-11行中调用了freenect.launch，参考freenect_launch/exampl/中的freenect-xyz.launch这个例程，通过设置参数决定你要启动的节点，同时该话题默认启动TF和Point；

        第17-22行是为激光生成包的参数设置，image和camera_info是depthimage_to_laserscan节点订阅的topic，需要通过remap链接到你自己的平台；scan是depthimage_to_laserscan节点发布的topic，输出直接可用的伪激光数据。

        0x04 打开fake_laser.launch启动文件和rqt_rviz并添加laserscan到display窗口

    roslaunch your_workspace/fake_laser.launch

        应该得到类似下图的状态

![](https://assets.bookshiyi.com/photo/2017/04/fake_laser_rviz_preview.png)

* * *

**常见问题**：

        如果没有得到伪激光数据可以尝试运行如下命令：

    rosnode info /depthimage_to_laserscan

        根据下图红色标注的位置辅助你判断问题所在：

![](https://assets.bookshiyi.com/photo/2017/04/rosnode_info_depthimage_to_laserscan.jpg)

* * *

**freenect启动文件特性浅析**：

*   freenect_camera freenect_nod发布的话题非常少，但是不包含TF数据的发布，需要自己另外发布TF；
*   freenect_launch freenect.launch发布的话题足够多，但是如果我们不关闭一些话题会导致系统资源的浪费；
*   freenect_launch freenect_launch/example下的launch文件可以参考

    **PS：pointcloud_to_laserscan**效果可能也不错，将在接下来进行测试。

* * *

最后感谢FireFly团队提供的**RK3399**高性能、奢侈配置的开发板(点击图片了解详情)：

[![](https://assets.bookshiyi.com/photo/2017/04/firefly_rk3399_preview.png)](http://www.t-firefly.com/zh/firenow/Firefly-rk3399/)

* * *

`