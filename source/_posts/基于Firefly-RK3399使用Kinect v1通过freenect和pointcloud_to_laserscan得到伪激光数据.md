---
title: 基于Firefly-RK3399使用Kinect v1通过freenect和pointcloud_to_laserscan得到伪激光数据
tags:
  - fake_laser
  - freenect
  - kinect
  - laserscan
  - point
  - rgbd
  - rk3399
  - 深度
  - 点云
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 只文本模式
  - 开源
  - 开源软件
  - 机器人
  - 深度传感器
date: 2017-04-06 16:05:47
---

#### 开发环境：**Firefly-RK3399** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **Kinect V1**

 

0x00 开始前请确保你的Kinect v1通过USB2.0与ROS计算机相连接，并且Kinect v1的电源功率足够；

0x01 确保已经安装**freenect**（如果没安装请移步[freenect安装教程](https://assets.bookshiyi.com/archives/1571)）；

0x02 安装**pointcloud\_to\_laserscan：**

方式一：源码安装（编译缺少tf2\_sensor\_msg）

    cd ~/catkin_ws/src  
    git clone --branch indigo-devel https://github.com/ros-perception/pointcloud\_to\_laserscan.git  
    cd ..  
    catkin_make  

方式二：功能包安装(推荐)

    sudo apt-get install ros-<rosdistro>-pointcloud-to-laserscan

0x03 以下是基于freenect和pointcloud\_to\_laserscan的fake_laser.launch代码：

`target_frame: camera_link # Leave disabled to output scan in pointcloud frame transform_tolerance: 0.01 min_height: 0.0 max_height: 1.0 angle_min: -1.5708 # -M_PI/2 angle_max: 1.5708 # M_PI/2 angle_increment: 0.0087 # M_PI/360.0 scan_time: 0.3333 range_min: 0.45 range_max: 4.0 use_inf: true # Concurrency level, affects number of pointclouds queued for processing and number of threads used # 0 : Detect number of cores # 1 : Single threaded # 2->inf : Parallelism level concurrency_level: 1`

        第4-11行中调用了freenect.launch，参考freenect_launch/exampl/中的freenect-xyz.launch这个例程，通过设置参数决定你要启动的节点，同时该话题默认启动TF和Point；

        第17-41行是为激光生成包的参数设置，cloud\_in是pointcloud\_to\_laserscan节点订阅的topic，需要通过remap链接到你自己的平台；scan是pointcloud\_to_laserscan节点发布的topic，输出直接可用的伪激光数据。

        其中21-40行描述对于Kinect传输性能设置的参数，包括目标TF、变换容忍偏差、最大/小目标高度、最大/小角度、角度增量（决定laserscan输出点的密集程度）、扫描周期、最远/近距离等。

0x04 打开fake\_laser.launch启动文件和rqt\_rviz并添加laserscan到display窗口

    roslaunch your\_workspace/fake\_laser.launch

        应该得到类似下图的状态

![](https://assets.bookshiyi.com/photo/2017/04/pointclou_to_laserscan_rviz.png)

* * *

**常见问题**：

        如果没有得到伪激光数据可以尝试运行如下命令：

    rosnode info /pointcloud\_to\_laserscan

        观察pointcloud\_to\_laserscan节点是否成功的订阅了指定的点云topic。

 

* * *

        最后感谢FireFly团队提供的**RK3399**高性能、奢侈配置的开发板(点击图片了解详情)：

[![](https://assets.bookshiyi.com/photo/2017/04/firefly_rk3399_preview.png)](http://www.t-firefly.com/zh/firenow/Firefly-rk3399/)

* * *

    sudo apt-get install(安装) ros-hydro-image-transport-plgins