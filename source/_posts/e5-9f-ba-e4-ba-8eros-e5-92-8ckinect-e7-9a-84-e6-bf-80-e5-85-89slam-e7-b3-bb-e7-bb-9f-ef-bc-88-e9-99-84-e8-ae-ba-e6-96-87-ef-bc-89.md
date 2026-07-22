---
title: 基于ROS和Kinect的激光SLAM系统（附论文）
tags:
  - kinect
  - ROS
  - slam
  - 激光
url: 1858.html
id: 1858
comments: false
categories:
  - ROS机器人操作系统
  - 同步定位与建图
  - 机器人
  - 深度传感器
  - 移动平台
date: 2017-04-21 09:54:46
---

        ROS机器人制作指南（更新中）：[http://bookshiyi.com/robotics/ros\_robot\_guide](http://bookshiyi.com/robotics/ros_robot_guide)

        **论文下载**：[本科毕业论文_基于ROS和RGB-D传感器的SLAM智能机器人.pdf](https://assets.bookshiyi.com/doc/%E6%9C%AC%E7%A7%91%E6%AF%95%E4%B8%9A%E8%AE%BA%E6%96%87_%E5%9F%BA%E4%BA%8EROS%E5%92%8CRGB-D%E4%BC%A0%E6%84%9F%E5%99%A8%E7%9A%84SLAM%E6%99%BA%E8%83%BD%E6%9C%BA%E5%99%A8%E4%BA%BA_OARAP_org.pdf)（可右键另存为）

        **ROS源码**：[https://github.com/bookshiyi/robot_ros](https://github.com/bookshiyi/robot_ros)

**        STM32源码**：[https://github.com/bookshiyi/robot_stm32](https://github.com/bookshiyi/robot_stm32)

##### 勘误：2018.09.04 文中提到“树莓派3B+”实为笔误，论文撰写时实际使用为树莓派3B，为避免误导读者，特此声明。感谢来自西南交通大学的章老师指出。

#### **演示视频**

* * *

<video controls preload="metadata" style="width: 100%; max-width: 800px;">
  <source src="https://assets.bookshiyi.com/video/%E5%9F%BA%E4%BA%8EROS%E5%92%8CKinect%E7%9A%84%E6%BF%80%E5%85%89SLAM_bookshiyi_com.mp4" type="video/mp4">
</video>

#### **作品实拍**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/ros_kinect_slam_robot_physical_figure_1.jpg)

![](https://assets.bookshiyi.com//photo/2017/04/ros_kinect_slam_robot_physical_figure_2.jpg)

![](https://assets.bookshiyi.com/photo/2017/04/ros_kinect_slam_robot_physical_figure_3.jpg)

![](https://assets.bookshiyi.com/photo/2017/04/ros_kinect_slam_robot_power_unit_physical_figure.jpg)

#### **硬件框图**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/ros_kinect_gmapping_slam.png)

#### **软件框图**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/ros_kinect_gmapping_slam_software.png)

#### **下位机PCB**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/robot_driver_board_pcb_preview.png)

![](https://assets.bookshiyi.com/photo/2017/04/robot_driver_board_pcb_physical_figure.png)

#### **场地实拍**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/jingyuan116_pic.png)

#### **栅格地图**

（栅格地图中蓝色箭头表示上图的拍摄位置及角度）

* * *

![](https://assets.bookshiyi.com/photo/2017/04/jingyuan116_map.png)

#### **节点关系**

* * *

#### ![](https://assets.bookshiyi.com/photo/2017/04/gmapping_node_topic_relation.png)

#### **致谢**

* * *

![](https://assets.bookshiyi.com/photo/2017/04/thanks.png)
