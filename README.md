# Apollo

[![Build Status](https://travis-ci.org/ApolloAuto/apollo.svg?branch=master)](https://travis-ci.org/ApolloAuto/apollo) [![Simulation Status](https://azure.apollo.auto/dailybuildstatus.svg)](https://azure.apollo.auto/dailybuild)

```
We choose to go to the moon in this decade and do the other things,
not because they are easy, but because they are hard.
-- John F. Kennedy, 1962
```

Welcome to the Apollo GitHub.

[Apollo](http://apollo.auto) 开源自动驾驶平台. 
It is a high performance flexible architecture which supports fully autonomous driving capabilities.
For business contact, please visit http://apollo.auto

**Apollo Team now proudly presents to you the latest [version 2.5](https://github.com/ApolloAuto/apollo/releases/tag/v2.5.0).**

## 安装

推荐在 Docker environment 中安装

The steps are:
 - 1. Run a machine that runs linux (tested on Ubuntu 16.04 with and without an nVidia GPU)
 - 2. Create a docker environment
 - 3. Build Apollo from source
 - 4. Bootstrap start Apollo
 - 5. Download the demonstration loop and run it
 - 6. Start a browser session and see the Dreamview user interface

More instructions are below

###  docker environment 安装

First, you need to [install docker-ce properly](https://github.com/ApolloAuto/apollo/blob/master/docker/scripts/README.md#install-docker).
The following scripts will get you into the container

```
docker ps  # to verify docker works without sudo
bash docker/scripts/dev_start.sh
# if in China, you had better use:bash docker/scripts/dev_start.sh -C to download from the server of docker in china.
bash docker/scripts/dev_into.sh

```

### 源码编译 apollo
    First check and make sure you are in development docker container before you proceed. 
    Now you will need to build from the source. 
    If you want to run the entire system, make sure you have an
    nVidia GPU and that you have installed the Linux nVidia drivers.

```
# To get a list of build commands
./apollo.sh
# To make sure you start clean
./apollo.sh clean
# This will build the full system and requires that you have an nVidia GPU with nVidia drivers loaded
bash apollo.sh build
```

If you do not have an nVidia GPU, the system will run but with the CUDA-based perception and other modules. 

You mustspecify either `dbg` for debug mode or `opt` for optimized code

```
./apollo.sh build_no_perception dbg
```

If you make modifications to the Dreamview frontend, then you must run `./apollo.sh build_fe`  before you run the
full build.


## 运行 Apollo

Follow the steps below to launch Apollo. Note that you must build the system first before you run it.
Note that the bootstrap.sh will actually succeed but the user interface will not come up if you skip the build step.

### Start Apollo

Running Apollo will start the ROS core and then startup a web user interface called Dreamview, 
this is handled by the bootstrap script, so from within the docker container, you should run:

```
# start module monitor
bash scripts/bootstrap.sh
```

### Access Dreamview
    Access Dreamview by opening your favorite browser, e.g. Chrome, go to http://localhost:8888 
    and you should see this screenHowever, there will be nothing running in the system.

![Access Dreamview](docs/demo_guide/images/apollo_bootstrap_screen.png)

### Select Drive Mode
From the dropdown box selet "Navigation" mode.

![Navigation Mode](docs/demo_guide/images/dreamview_2_5_setup_profile.png)


### Replay demo rosbag

To see if the system works, use the demo 'bag' which feeds the system.

```
# get rosbag note that the command download is required
python ./docs/demo_guide/rosbag_helper.py demo_2.5.bag

# You can now replay this demo "bag" in a loop with the '-l' flag
rosbag play -l demo_2.5.bag
```

Dreamview should show a running vehicle now. (The following image might be different due to changes in frontend.)

![Dreamview with Trajectory](docs/demo_guide/images/dv_trajectory_2.5.png)

## Documents

Apollo documents can be found under the [docs](https://github.com/ApolloAuto/apollo/blob/master/docs/) repository.
   * [quickstart](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/): the quickstart tutorial.
   * [demo_guide](https://github.com/ApolloAuto/apollo/blob/master/docs/demo_guide/): the guide for demonstration.
   * [![Apollo Offline Demo](https://img.youtube.com/vi/Q4BawiLWl8c/0.jpg)](https://www.youtube.com/watch?v=Q4BawiLWl8c)
   * [how to contribute code](https://github.com/ApolloAuto/apollo/blob/master/CONTRIBUTING.md): the guide for contributing code to Apollo.
   * [howto](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/): tutorials on how to build, run and modify codes.
   * [specs](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/): Specification documents of Apollo.
   * [Doxygen APIs](https://apolloauto.github.io/doxygen/apollo/): Apollo Doxygen pages

## Ask Questions

You are welcome to submit questions and bug reports as [Github Issues](https://github.com/ApolloAuto/apollo/issues).

## Copyright and License

Apollo is provided under the [Apache-2.0 license](LICENSE).

## Disclaimer
Please refer the Disclaimer of Apollo in [Apollo official website](http://apollo.auto/docs/disclaimer.html).
# ===========================
# Apollo 3.0 技术指南

## 概况
> 了解Apollo3.0基础概念和Apollo3.0快速入门指南

  * [Apollo 3.0快速入门指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_3_0_quick_start_cn.md)
  
## 硬件和系统安装
> 了解Apollo3.0硬件和系统安装过程

  * [Apollo 3.0硬件和系统安装指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_3_0_hardware_system_installation_guide_cn.md)

## 校准
> 了解校准的过程

  * [Apollo激光雷达校准指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_1_5_lidar_calibration_guide_cn.md)
  * [Apollo 2.0传感器校准指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_2_0_sensor_calibration_guide_cn.md)
  * [多激光雷达全球导航卫星系统(Multiple-LiDAR GNSS)校准指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/multiple_lidar_gnss_calibration_guide_cn.md)
  * [Apollo坐标系统](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/coordination_cn.md)

## 软件安装
> 了解Apollo3.0的软件安装过程

  * [Apollo软件安装指南](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_software_installation_guide_cn.md)
  * [如何调试Dreamview启动问题](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_debug_dreamview_start_problem_cn.md)
  * [运行线下演示](https://github.com/ApolloAuto/apollo/blob/master/docs/demo_guide/README_cn.md)
  
## Apollo系统架构和原理
> 了解核心模块的架构和原理

  * [Apollo 3.0 软件架构](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/Apollo_3.0_Software_Architecture_cn.md "Apollo software architecture")
  * [3D 障碍物感知](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/3d_obstacle_perception_cn.md)
  * [Apollo 3.0感知](https://github.com/ApolloAuto/apollo/blob/master/modules/perception/README.md)
  * [二次规划（QP）样条路径优化](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/qp_spline_path_optimizer_cn.md)
  * [二次规划（QP）样条ST速度优化](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/qp_spline_st_speed_optimizer_cn.md)
  * [参考线平滑设定](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/reference_line_smoother_cn.md)
  * [交通信号灯感知](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/traffic_light_cn.md)
  
## 功能模块和相关扩展知识
> 了解Apollo功能模块和相关扩展知识

  * [控制总线模块](https://github.com/ApolloAuto/apollo/blob/master/modules/canbus/README.md)
  * [通用模块](https://github.com/ApolloAuto/apollo/blob/master/modules/common/README.md)
  * [控制模块](https://github.com/ApolloAuto/apollo/blob/master/modules/control/README.md)
  * [数据模块](https://github.com/ApolloAuto/apollo/blob/master/modules/data/README.md)
  * [定位模块](https://github.com/ApolloAuto/apollo/blob/master/modules/localization/README.md)
  * [感知模块](https://github.com/ApolloAuto/apollo/blob/master/modules/perception/README.md)
  * [Planning模块](https://github.com/ApolloAuto/apollo/blob/master/modules/planning/README.md)
  * [预测模块](https://github.com/ApolloAuto/apollo/blob/master/modules/prediction/README.md)
  * [寻路模块](https://github.com/ApolloAuto/apollo/blob/master/modules/routing/README.md)

  * [如何添加新的GPS接收器](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_gps_receiver_cn.md)
  * [如何添加新的CAN卡](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_new_can_card_cn.md )
  * [如何添加新的控制算法](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_new_control_algorithm_cn.md)
  * [如何在预测模块中添加新评估器](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_new_evaluator_in_prediction_module_cn.md)
  * [如何在预测模块中添加一个预测器](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_new_predictor_in_prediction_module_cn.md)
  * [如何在Apollo中添加新的车辆](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_a_new_vehicle_cn.md)
  * [如何添加新的外部依赖项](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_add_an_external_dependency_cn.md)
  
  ## 开发者工具
> 了解开发者工具

  * [使用VSCode构建、调试Apollo项目](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/how_to_build_and_debug_apollo_in_vscode_cn.md "How  to build and debug Apollo in VSCode")
  * [DreamView用法介绍](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/dreamview_usage_table_cn.md)



# ===============================
# Apollo具体内容说明

## 软件
- [Apollo 2.0软件系统架构](Apollo_2.0_Software_Architecture.md)
- [Apollo 3.0软件系统架构](Apollo_3.0_Software_Architecture_cn.md)
- [Planning模块架构概述](Class_Architecture_Planning_cn.md)

## Apollo硬件开发平台

我们强烈建议使用者在阅读硬件开发平台文档前浏览我们的免责声明。

- [Apollo传感器单元（ASU）](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Apollo_Sensor_Unit/Apollo_Sensor_Unit_Installation_Guide_cn.md)
- [摄像机](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Camera/README.md)
- [激光雷达](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Lidar/README.md)
- [雷达](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Radar/README.md)
- [导航](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Navigation/README_cn.md)
- [IPC](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/IPC/Nuvo-6108GC_Installation_Guide_cn.md)
- [软件系统和内核安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Software_and_Kernel_Installation_guide_cn.md)

## 感知

- [Apollo 2.5感知系统](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/perception_apollo_2.5.md)
- [Apollo 2.5传感器安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Guideline_sensor_Installation_apollo_2.5.md)
- [Apollo 3.0感知系统]https://github.com/ApolloAuto/apollo/tree/master/docs/specs/(perception_apollo_3.0_cn.md)
- [Apollo 3.0传感器安装指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/Guideline_sensor_Installation_apollo_3.0_cn.md)
- [激光雷达校准英文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/lidar_calibration.pdf)
- [激光雷达校准中文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/lidar_calibration_cn.pdf)

## HMI
- [Dreamview使用方法](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/dreamview_usage_table_cn.md)

## 算法
- [三维障碍物感知英文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/3d_obstacle_perception.md)
- [三维障碍物感知中文版](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/3d_obstacle_perception_cn.md)
- [二次规划路径样条优化](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/qp_spline_path_optimizer_cn.md)
- [二次规划st速度样条优化](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/qp_spline_st_speed_optimizer_cn.md)
- [参考线平滑设定](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/reference_line_smoother_cn.md)
- [交通信号灯感知](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/traffic_light_cn.md)

## 其他通用知识
- [坐标系统](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/coordination_cn.md)
- [Apollo安全更新SDK用户指南](https://github.com/ApolloAuto/apollo/tree/master/docs/specs/apollo_secure_upgrade_user_guide-CN.md)


# ===============================
# 工业级PC（IPC）软件安装指南

本文档介绍下述软件的安装步骤：

- Ubuntu Linux
- Apollo Kernel
- Nvidia GPU Driver

![tip_icon](images/tip_icon.png)成功完成本文档中介绍的软件安装需要使用者有使用Linux系统的经验。

## 安装Unbuntu Linux

按照如下步骤执行：

1. 创建一个可引导的Ubuntu Linux USB启动盘：

   下载Ubuntu 14.04（或其他的变种系统如Xubuntu）并[创建一个可引导的USB启动盘](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-ubuntu#0)。我们推荐使用Ubuntu 14.04。在系统启动时按下F2（或其他按键，请参考系统文档）进入BIOS设置，我们建议禁用Quick Boot和Quiet Boot设置以更容易的在启动时捕获错误信息。
   
2. 安装Ubuntu Linux：

   a.   将安装Unbuntu的USB启动盘插入USB接口中并启动系统
   
   b.   按照屏幕提示执行安装
   
3. 执行软件更新：

   a.   安装结束后重启并进入系统
   
   b.   启动Software Update并更新到最新软件包，或在终端程序如GNOME Terminal中执行下述指令完成更新：

   ```shell
   sudo apt-get update; sudo apt-get upgrade
   ```
   
   c. 启动终端程序如GNOME Terminal，执行下述指令安装Linux 4.4内核
   
   ```shell
   sudo apt-get install linux-generic-lts-xenial
   ```
   
   ![tip_icon](images/tip_icon.png)IPC必须有网络连接以更新和安装软件。确保IPC的以太网线接入了有互联网访问权限的网络。如果接入的网络没有使用动态主机配置协议（DHCP），使用者可能需要对IPC的网络进行配置。

## 安装Apollo内核

Apollo在车辆上的运行需要[Apollo内核](https://github.com/ApolloAuto/apollo-kernel)。我们强烈推荐安装预先构建的内核版本。

##  使用预先构建的内核版本

使用者使用下述指令获取和安装预先构建的内核版本。

1. 从GitHub下载发布版本包：

```
https://github.com/ApolloAuto/apollo-kernel/releases
```

2. 成功下载发布版本包后安装内核：

```
tar zxvf linux-4.4.32-apollo-1.5.0.tar.gz
cd install
sudo bash install_kernel.sh
```

3. 使用 `reboot` 指令重启系统
4. 【可选步骤-如果使用者使用了CAN卡】参考CAN卡供应商提供的指令构建CAN卡驱动程序

##  构建个人的内核版本

如果使用者修改了内核，或者预先构建的版本对使用者的工作平台不是最好的选择，使用者可以使用下述指令构建个人的内核版本：

1. 从资源库中clone源代码

```
git clone https://github.com/ApolloAuto/apollo-kernel.git
cd apollo-kernel
```

2. 参考CAN卡供应商提供的指令加入CAN卡驱动的源代码
3. 使用下述指令构建内核：

```
bash build.sh
```

4. 参考上面章节中介绍的如何安装预先构建内核版本的步骤进行内核的安装

## 安装NVIDIA GPU驱动

Apollo在车辆上的运行需要[NVIDIA GPU驱动](http://www.nvidia.com/download/driverResults.aspx/114708/en-us)。使用者必须使用指定的参数选项安装NVIDIA GPU驱动。

1. 下载安装文件

```
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/375.39/NVIDIA-Linux-x86_64-375.39.run
```

2. 执行驱动安装

```
sudo bash ./NVIDIA-Linux-x86_64-375.39.run --no-x-check -a -s
```

##  参考资料

1. [Ubuntu官方网站](https://www.ubuntu.com/desktop)


# =============================
# Apollo 3.0 软件架构

自动驾驶Apollo3.0核心软件模块包括：

- **感知** — 感知模块识别自动驾驶车辆周围的世界。感知中有两个重要的子模块：障碍物检测和交通灯检测。
- **预测** — 预测模块预测感知障碍物的未来运动轨迹。
- **路由** — 路由模块告诉自动驾驶车辆如何通过一系列车道或道路到达其目的地。
- **规划** — 规划模块规划自动驾驶车辆的时间和空间轨迹。
- **控制** — 控制模块通过产生诸如油门，制动和转向的控制命令来执行规划模块产生的轨迹。
- **CanBus** — CanBus是将控制命令传递给车辆硬件的接口。它还将底盘信息传递给软件系统。
- **高精地图** — 该模块类似于库。它不是发布和订阅消息，而是经常用作查询引擎支持，以提供关于道路的特定结构化信息。
- **定位** — 定位模块利用GPS，LiDAR和IMU的各种信息源来定位自动驾驶车辆的位置。
- **HMI** — Apollo中的HMI和DreamView是一个用于查看车辆状态，测试其他模块以及实时控制车辆功能的模块.
- **监控** — 车辆中所有模块的监控系统包括硬件。
- **Guardian** — 新的安全模块，用于干预监控检测到的失败和action center相应的功能。
执行操作中心功能并进行干预的新安全模块应监控检测故障。

```
注意：下面列出了每个模块的详细信息。
```

这些模块的交互如下图所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/Apollo_3.0_SW.png)

每个模块都作为单独的基于CarOS的ROS节点运行。每个模块节点都发布和订阅特定topic。订阅的topic用作数据输入，而发布的topic用作数据输出。以下各节详细介绍了各模块情况。

## 感知

感知依赖LiDAR点云数据和相机原始数据。除了这些传感器数据输入之外，交通灯检测依赖定位以及HD-Map。由于实时ad-hoc交通灯检测在计算上是不可行的，因此交通灯检测需要依赖定位确定何时何地开始通过相机捕获的图像检测交通灯。
对Apollo 3.0的更改：
  - CIPV检测/尾随 - 在单个车道内移动。
  - 全线支持 - 粗线支持，可实现远程精确度。相机安装有高低两种不同的安装方式。
  - 异步传感器融合 – 因为不同传感器的帧速率差异——雷达为10ms，相机为33s，LiDAR为100ms，所以异步融合LiDAR，雷达和相机数据，并获取所有信息并得到数据点的功能非常重要。
  - 在线姿态估计 - 在出现颠簸或斜坡时确定与估算角度变化，以确保传感器随汽车移动且角度/姿态相应地变化。
  - 视觉定位 – 基于相机的视觉定位方案正在测试中。
  - 超声波传感器 – 作为安全保障传感器，与Guardian一起用于自动紧急制动和停车。

## 预测

预测模块负责预测所有感知障碍物的未来运动轨迹。输出预测消息封装了感知信息。预测订阅定位和感知障碍物消息，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/prediction.png)

当接收到定位更新时，预测模块更新其内部状态。当感知发出其发布感知障碍物消息时，触发预测实际执行。

## 定位

定位模块聚合各种数据以定位自动驾驶车辆。有两种类型的定位模式：OnTimer和多传感器融合。

第一种基于RTK的定位方法，通过计时器的回调函数“OnTimer”实现，如下所示。
![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/localization.png)

另一种定位方法是多传感器融合（MSF）方法，其中注册了一些事件触发的回调函数，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/localization_2.png)

## 路由
为了计算可通行车道和道路，路由模块需要知道起点和终点。通常，路由起点是自动驾驶车辆位置。重要的数据接口是一个名为`OnRoutingRequest`的事件触发函数，其中`RoutingResponse`的计算和发布如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/routing.png)

## 规划
Apollo 2.0需要使用多个信息源来规划安全无碰撞的行驶轨迹，因此规划模块几乎与其他所有模块进行交互。

首先，规划模块获得预测模块的输出。预测输出封装了原始感知障碍物，规划模块订阅交通灯检测输出而不是感知障碍物输出。
然后，规划模块获取路由输出。在某些情况下，如果当前路由结果不可执行，则规划模块还可以通过发送路由请求来触发新的路由计算。

最后，规划模块需要知道定位信息（定位：我在哪里）以及当前的自动驾驶车辆信息（底盘：我的状态是什么）。规划模块由固定频率触发，主数据接口是调用`RunOnce`函数的`OnTimer`回调函数。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/planning_1.png)

底盘，定位，交通灯和预测等数据依赖关系通过`AdapterManager`类进行管理。核心软件模块同样也由`AdapterManager`类管理。例如，定位通过`AdapterManager :: GetLocalization()`管理，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/planning_2.png)

## 控制
如规划模块中所述，控制将规划轨迹作为输入，并生成控制命令传递给CanBus。它有三个主要的数据接口：OnPad，OnMonitor和OnTimer。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/control_1.png)

`OnPad`和`OnMonitor`是仿真和HMI的交互接口。 主要数据接口是`OnTimer`，它定期产生实际的控制命令，如下所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/control_2.png)

## CanBus

CanBus有两个数据接口。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/canbus_1.png)

第一个数据接口是基于计时器的发布者，回调函数为“OnTimer”。如果启用，此数据接口会定期发布底盘信息。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/canbus_2.png)

第二个数据接口是一个基于事件的发布者，回调函数为“OnControlCommand”，当CanBus模块接收到控制命令时会触发该函数。


## HMI
Apollo中的HMI或DreamView是一个Web应用程序：
     - 可视化自动驾驶模块的输出，例如，规划轨迹，汽车定位，底盘状态等。
     - 为用户提供人机交互界面，以查看硬件状态，打开/关闭模块，以及启动自动驾驶汽车。
     - 提供调试工具，如PnC Monitor，以有效跟踪模块问题。

## 监控
包括硬件在内的，车辆中所有模块的监控系统。监控模块从其他模块接收数据并传递给HMI，以便司机查看并确保所有模块都正常工作。如果模块或硬件发生故障，监控会向Guardian（新的操作中心模块）发送警报，然后决定需要采取哪些操作来防止系统崩溃。

## Guardian
这个新模块根据Monitor发送的数据做出相应决定。Guardian有两个主要功能：
     - 所有模块都正常工作 - Guardian允许控制模块正常工作。控制信号被发送到CANBus，就像Guardian不存在一样。
     - 监控检测到模块崩溃 - 如果监控检测到故障，Guardian将阻止控制信号到达CANBus并使汽车停止。 Guardian有三种方式决定如何停车并会依赖最终的Gatekeeper——超声波传感器，
         - 如果超声波传感器运行正常而未检测到障碍物，Guardian将使汽车缓慢停止
         - 如果传感器没有响应，Guardian会硬制动，使车马上停止。
         - 这是一种特殊情况，如果HMI通知驾驶员即将发生碰撞并且驾驶员在10秒内没有干预，Guardian会使用硬制动使汽车立即停止。

```
注意: 
1.在上述任何一种情况下，如果Monitor检测到任何模块或硬件出现故障，Guardian将始终停止该车。
2.监控器和Guardian解耦以确保没有单点故障，并且可以为Guardian模块添加其他行为且不影响监控系统，监控还与HMI通信。
```

# =======================
# 感知
Apollo 3.0
June 27, 2018

## 简介
    Apollo 3.0 主要针对采用低成本传感器的L2级别自动驾驶车辆。
    在车道中的自动驾驶车辆通过一个前置摄像头和前置雷达要与关键车辆（在路径上最近的车辆）保持一定的距离。
    Apollo 3.0 支持在高速公路上不依赖地图的高速自动驾驶。
    深度网路学习处理图像数据，随着搜集更多的数据，深度网络的性能随着时间的推移将得到改善。


***安全警告***
    Apollo 3.0 不支持没有包含本地道路和说明标示的急转弯道路。
    感知模块是基于采用深度网络并结合有限数据的可视化检测技术。
    因此，在我们发布更好的网络之前，驾驶员应该小心驾驶并控制好车辆方向而不能依赖与自动驾驶。
    请在安全和限制区域进行试驾。

- ***推荐道路***
	- ***道路两侧有清晰的白色车道线***

- ***禁止***
	- ***急转弯道路***
	- ***没有车道线标记的道路***
	- ***路口***
	- ***对接点或虚线车道线***
	- ***公共道路***

## 感知模块
每个模块的流程图如下所示。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_flow_chart_apollo_3.0.png)

**图 1: Apollo 3.0的流程图**

### 深度网络
    深度网络摄取图像并为Apollo 3.0提供两个检测输出，车道线和对象。
    目前，对深度学习中使用单一任务还是协同训练任务还存在一些争议。
    诸如车道检测网络或物体检测网络的单一网络通常比一个协同训练的多任务网络执行得更好。
    然而，在给定有限资源的情况下，多个单独的网络将是昂贵的并且在处理中消耗更多时间。
    因此，对于经济设计而言，协同训练是不可避免的，并且在性能上会有一些妥协。
    在 Apollo 3.0, YOLO [1][2] 被用作对象和车道线检测的基础网络。
    该对象具有车辆、卡车、骑车人和行人类别，并由表示成具有方向信息的2-D边界框。
    通过使用具有一些修改的相同网络进行分段来检测车道线。
    对于整条车道线，我们有一个单独的网络，
    以提供更长的车道线，无论是车道线是离散的还是连续的。


### 物体识别/跟踪
    在交通场景中，有两类物体: 静态物体和动态物体。
    静态物体包括车道线、交通信号灯以及数以千计的以各种语言写成的交通标示。
    除了驾驶之外，道路上还有多个地标，主要用于视觉定位，包括路灯，障碍物，道路上的桥梁或任何天际线。
    对于静态物体，Apollo 3.0将仅检测车道线.

    在动态物体中，Apollo在路上关心乘用车，卡车，骑自行车者，行人或任何其他物体，包括动物或身体部位。
    Apollo还可以根据物体所在的车道对物体进行分类。
    最重要的物体是CIPV（路径中最近的物体）。下一个重要对象将是相邻车道中的物体。


#### 2D-to-3D 边界框
    给定一个2D盒子，其3D大小和相机方向，该模块搜索相机坐标系统中的3D位置，
    并使用该2D盒子的宽度，高度或2D区域估计精确的3D距离。
    该模块可在没有准确的外部相机参数的情况下工作。

#### 对象跟踪
    对象跟踪模块利用多种信息，例如3D位置，2D图像补丁，2D框或深度学习ROI特征。
    跟踪问题通过有效地组合线索来表达为多个假设数据关联，
    以提供路径和检测到的对象之间的最正确关联，从而获得每个对象的正确ID关联。

### 车道检测/追踪
    在静态对象中，我们在Apollo 3.0中将仅处理通道线。
    该车道用于纵向和横向控制。
    车道本身引导横向控制，并且在车道内的对象引导纵向控制。

#### 车道线
    我们有两种类型的车道线，车道标记段和整个车道线。
    车道标记段用于视觉定位，整个车道线用于使车辆保持在车道内。
    该通道可以由多组折线表示，例如下一个左侧车道线，左侧线，右侧线和下一个右侧线。
    给定来自深度网络的车道线热图，通过阈值化生成分段的二进制图像。
    该方法首先找到连接的组件并检测内部轮廓。
    然后，它基于自我车辆坐标系的地面空间中的轮廓边缘生成车道标记点。
    之后，它将这些车道标记与具有相应的相对空间（例如，左（L0），右（R0），下左（L1），下（右）（L2）等）标签的若干车道线对象相关联。

### CIPV (最近路径车辆)
    CIPV是当前车道中最接近的车辆。
    对象由3D边界框表示，其从上到下视图的2D投影将对象定位在地面上。
    然后，检查每个对象是否在当前车道中。
    在当前车道的对象中，最接近的一个将被选为CIPV。

### 跟车
    跟车是跟随前车的一种策略。
    从跟踪对象和当前车辆运动中，估计对象的轨迹。
    该轨迹将指导对象如何在道路上作为一组移动并且可以预测未来的轨迹。
    有两种跟车尾随，一种是跟随特定车辆的纯尾随，
    另一种是CIPV引导的尾随，当检测到无车道线时，当前车辆遵循CIPV的轨迹。 

输出可视化的快照如图2所示。 
![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_visualization_apollo_3.0.png)

**图 2: Apollo 3.0中感知输出的可视化。左上角是基于图像的输出。左下角显示了对象的3D边界框。左图显示了车道线和物体的三维俯视图。CIPV标有红色边框。黄线表示每辆车的轨迹**

### 雷达 + 摄像头融合
    给定多个传感器，它们的输出应以协同方式组合。
    Apollo 3.0，介绍了一套带雷达和摄像头的传感器。
    对于此过程，需要校准两个传感器。每个传感器都将使用Apollo 2.0中介绍的相同方法进行校准。
    校准后，输出将以3-D世界坐标表示，每个输出将通过它们在位置，大小，时间和每个传感器的效用方面的相似性进行融合。
    在学习了每个传感器的效用函数后，摄像机对横向距离的贡献更大，雷达对纵向距离测量的贡献更大。
    异步传感器融合算法也作为选项提供。

### 伪车道
    所有车道检测结果将在空间上临时组合以诱导伪车道，
    该车道将被反馈到规划和控制模块。
    某些车道线在某帧中不正确或缺失。
    为了提供平滑的车道线输出，使用车辆里程测量的历史车道线。
    当车辆移动时，保存每个帧的里程表，并且先前帧中的车道线也将保存在历史缓冲器中。
    检测到的与历史车道线不匹配的车道线将被移除，历史输出将替换车道线并提供给规划模块。

### 超声波传感器
    Apollo 3.0支持超声波传感器。每个超声波传感器通过CAN总线提供被检测对象的距离。
    来自每个超声波传感器的测量数据被收集并作为ROS主题广播。
    将来，在融合超声波传感器后，物体和边界的地图将作为ROS的输出发布。

## 感知输出
PnC的输入将与之前基于激光雷达的系统的输入完全不同。

- 车道线输出
	- 折线和/或多项式曲线
	- 车道类型按位置：L1（左下车道线），L0（左车道线），R0（右车道线），R1（右下车道线

- 对象输出
	- 3D长方体
	- 相对速度和方向
	- 类型：CIPV，PIHP，其他
	- 分类：汽车，卡车，自行车，行人
	- Drops：物体的轨迹

世界坐标是3D中的当前车辆坐标，其中后中心轴是原点。

## 参考
[1] J Redmon, S Divvala, R Girshick, A Farhadi, "你只看一次：统一的实时物体检测" CVPR 2016

[2] J Redmon, A Farhadi, "YOLO9000: 更好, 更快, 更强," arXiv preprint

# ===================================
# 交通信号灯感知

本文档详细的介绍了Apollo2.0中交通信号感知模块的工作原理。

## 简介

交通信号灯感知模块通过使用摄像头提供精确全面的路面交通信号灯状态。

通常情况下，交通信号灯有3种状态：

- 红
- 黄
- 绿

然而当信号灯不能正常工作时，它可能是黑色的或者闪烁着红灯或黄灯。有时候在摄像头的视野内找不到信号灯，从而导致无法正确检测信号灯状态。

为了覆盖全部的情况，交通信号灯感知模块提供了5种信号灯状态输出：

- 红
- 黄
- 绿
- 黑
- 未知

该模块的高精地图功能反复的检测车辆前方是否有信号灯出现。在给定车辆的位置后，可以通过查询高精地图获取信号灯的边界，并用边界上的4个点来表示信号灯。如果存在信号灯，则信号灯位置信息将从世界坐标系投射到图片坐标系。

Apollo已经证明了仅仅使用一个固定视野的摄像头无法识别所有的信号灯。存在这种限制的原因是：

- 感知范围应该大于100米
- 信号灯的高度和路口的宽度变化范围很大

结果是Apollo2.0使用了2个摄像头来扩大感知范围。

-  一个**远距摄像头**，焦距是25毫米，被用来观察前方远距离的信号灯。远距摄像头捕获的信号灯在图片上展现的非常大而且容易被检测。但是远距摄像头的视野有限制，如果路线不够直或者车辆太过于靠近信号灯，经常无法拍摄到信号灯。


- 一个**广角摄像头**。焦距是6毫米，是对远距摄像头视野不足的补充。

该模块会根据当前信号灯的投射状态决定使用哪个摄像头。虽然只有两个摄像头，但是该模块的算法被设计的可以控制多个摄像头。

下述图片展示了使用远距摄像头（上图）和广角摄像头（下图）检测到信号灯的图片。

![telephoto camera](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/traffic_light/long.jpg)


![wide angle camera](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/traffic_light/short.jpg)


# 数据管道

数据管道有两个主要的部分，会在下面章节中介绍
- 预处理阶段
  - 信号灯投射
  - 摄像头选择
  - 图像和信号灯缓存同步
- 处理阶段
  - 调整—提供精确的信号灯边界盒
  - 识别—提供每个边界盒的颜色
  - 修正—根据时间顺序关系修正颜色

## 预处理阶段

没有必要在每一帧的图像中去检测信号灯。信号灯的变化频率是很低的而且计算机的资源也有限。通常，从不同摄像头输入的图像信息会几乎同时的到达，但是只有一个会进入管道的处理阶段。因此图像的遴选和匹配是很必要的。

### 输入输出

本章节介绍了预处理阶段的输入输出数据。输入数据可以通过订阅Apollo相关模块数据来获得，或者直接读取本地的存储文件。输出数据被传输到下一层的处理阶段。

#### 输入数据

- 可以通过订阅以下topic来获取不同摄像头的图像数据：

    - `/apollo/sensor/camera/traffic/image_long`
    - `/apollo/sensor/camera/traffic/image_short`

- 定位信息，通过查询以下topic获得：
    - `/tf`

- 高精地图

- 校准结果

#### 输出数据

  - 被选择的摄像头输出的的图像信息
  - 从世界坐标系投射到图像坐标系的信号灯边界盒
  
### 摄像头选择
  
使用一个唯一的ID和其边界上的4个点来表示信号灯，每个点都是世界坐标系中的3维坐标点。

下例展示了一个典型的信号灯记录信息`signal info`。给出车辆位置后，4个边界点可以通过查询高精地图获得。

```protobuf
signal info:
id {
  id: "xxx"
}
boundary {
  point { x: ...  y: ...  z: ...  }
  point { x: ...  y: ...  z: ...  }
  point { x: ...  y: ...  z: ...  }
  point { x: ...  y: ...  z: ...  }
}
```

3维世界坐标系中的边界点随后被投射到每个摄像头图像的2维坐标系。对每个信号灯而言，远距摄像头图像上展示的4个投射点区域更大，这比广角摄像头更容易检测信号灯。最后会选择具有最长的焦距且能够看到所有信号灯的摄像头图片作为输出图像。投射到该图像上的信号边界盒将作为输出的边界盒。

被选择的摄像头的ID和时间戳缓存在队列中：


 ``` C++
struct ImageLights {
  CarPose pose;
  CameraId camera_id;
  double timestamp;
  size_t num_signal;
  ... other ...
};
 ```
 
 至此，我们需要的所有信息包括定位信息、校准结果和高精地图。因为投射不依赖于图像的内容，所以选择可以在任何时间完成。在图像信息到达时进行选择仅仅是为了简单。而且，并不是图像信息一到达就要进行选择，通常会设置选择的时间间隔。
 
 
### 图像同步

图像信息包含了摄像头ID和时间戳。摄像头ID和时间戳的组合用来找到可能存在的缓存信息。如果能在缓存区找到和该图像的摄像头ID一样且时间戳相差很小的缓存信息，则该图像会被传输到处理阶段。所有不合适的缓存信息会被丢弃。

## 处理阶段

该阶段分为3个步骤，每个步骤重点执行一个任务：

- 调整 — 在ROI中检测信号灯边界盒
- 识别 — 鉴别边界盒的颜色
- 修正 — 根据信号灯颜色的时间顺序关系修正颜色

### 输入输出

本章节介绍处理阶段的输入和输出数据。输入数据从预处理阶段获得，输出数据作为鉴别信号灯的结果。

#### 输入数据

- 被选择的摄像头图像信息
- 一组边界盒信息

#### 输出数据

  - 一组带有颜色标签的边界盒信息


### 调整

被定位信息、校准信息和高精地图信息影响的投射点 ***不是完全可靠的*** 。通过投射的信号灯位置计算的一个大的兴趣区域（Region of Interest ROI）被用来确定信号灯精确的边界盒。

在下述图片中，蓝色的长方形表示被投射的信号灯的边界盒，实际上和信号灯的准确位置有一定的偏差。大的黄色长方形是ROI。

![example](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/traffic_light/example.jpg)

信号灯检测是一个常规的卷积神经网络检测任务，它接收带有ROI信息的图像作为输入数据，顺序输出边界盒。输出结果中的信号灯数量可能多于输入数据。

Apollo会根据输入信号灯的位置、形状及检测的评分选择合适的信号灯。如果CNN在ROI内找不到任何的信号灯，则输入数据中的信号灯将被标记为未知，且跳过剩下的两个步骤。

### 识别

信号灯识别是一个常规的卷积神经网络鉴别任务，它接收带有ROI信息的图像和一组边界盒信息作为输入数据。输出数据是一个`$4\times n$ vector`， 表示每个边界盒是黑色、红色、黄色和绿色的概率。
当且仅当概率足够大时，有最大概率的类别会被识别为信号灯的状态。否则信号灯状态被设置为未知，表示状态未确定。

### 修正

因为信号灯可能会闪烁或者被遮挡，并且识别阶段也 ***并不是*** 完美的，输出的信号灯状态可能不是真正的状态。修正信号灯状态是很有必要的。

如果修正器接收到一个确定的信号灯状态例如红色或者绿色，则修正器保存该状态并直接输出。如果接收到黑色或者未知，修正器会检测状态保存列表。如果信号灯状态已经确定持续了一段时间，那么将保存的状态输出。否则将黑色或者未知输出。

因为时间顺序关系的存在，黄色只会在绿色之后红色之前出现，所以为了安全的考虑，在绿色出现之前任何红色之后的黄色都会被设置为红色。



3D 障碍物感知
====================

Apollo解决的障碍物感知问题：

- 高精地图ROI过滤器（HDMap ROI Filter）
- 基于卷积神经网络分割（CNN Segmentation）
- MinBox 障碍物边框构建（MinBox Builder）
- HM对象跟踪（HM Object Tracker）

高精地图ROI过滤器
-------------------------------------

ROI（The Region of Interest）指定从高精地图检索到包含路面、路口的可驾驶区域。高精地图 ROI 过滤器（往下简称“过滤器”）处理在ROI之外的激光雷达点，去除背景对象，如路边建筑物和树木等，剩余的点云留待后续处理。

给定一个高精地图，每个激光雷达点的关系意味着它在ROI内部还是外部。
每个激光雷达点可以查询一个车辆周围区域的2D量化的查找表（LUT）。过滤器模块的输入和输出汇总于下表。

  |输入                                                                     |输出                                                                     |
  |------------------------------------------------------------------------- |---------------------------------------------------------------------------|
  |点云: 激光雷达捕捉的3D点数据集           | 由高精地图定义的ROI内的输入点索引。      |
  |高精地图: 多边形集合，每个多边形均含有一个有序的点集。     |                                       |
 
一般来说，Apollo 高精地图 ROI过滤器有以下三步：

1. 坐标转换
2. ROI LUT构造
3. ROI LUT点查询

### 坐标转换

对于（高精地图ROI）过滤器来说，高精地图数据接口被定义为一系列多边形集合，每个集合由世界坐标系点组成有序点集。高精地图ROI点查询需要点云和多边形处在相同的坐标系，为此，Apollo将输入点云和HDMap多边形变换为来自激光雷达传感器位置的地方坐标系。

### ROI LUT构造

Apollo采用网格显示查找表（LUT），将ROI量化为俯视图2D网格，以此决定输入点是在ROI之内还是之外。

如图1所示，该LUT覆盖了一个矩形区域，该区域位于高精地图边界上方，以普通视图周围的预定义空间范围为边界。它代表了与ROI关联网格的每个单元格（如用1/0表示在ROI的内部/外部）。 为了计算效率，Apollo使用 **扫描线算法**和 **位图编码**来构建ROI LUT。

<img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/roi_lookup_table.png">
<div align=center>图 1 ROI显示查找表（LUT）</div>

蓝色线条标出了高精地图ROI的边界，包含路表与路口。红色加粗点表示对应于激光雷达传感器位置的地方坐标系原始位置。2D网格由8*8个绿色正方形组成，在ROI中的单元格，为蓝色填充的正方形，而之外的是黄色填充的正方形。

### ROI LUT点查询

基于ROI LUT，查询每个输入点的关系使用两步认证。对于点查询过程，Apollo数据编译输出如下，:

1. 检查点在ROI LUT矩形区域之内还是之外。
2. 查询LUT中相对于ROI关联点的相应单元格。
3. 收集属于ROI的所有点，并输出其相对于输入点云的索引。

用户定义的参数可在配置文件`modules/perception/model/hdmap_roi_filter.config`中设置，HDMap ROI Filter 参数使用参考如下表格：

  |参数名称      |使用                                                                          |默认     |
  |------------------- |------------------------------------------------------------------------------ |------------|
  |range           | 基于LiDAR传感器点的2D网格ROI LUT的图层范围），如(-70, 70)*(-70, 70) |70.0 米 |
  |cell_size           | 用于量化2D网格的单元格的大小。                                   |0.25 米  |
  |extend_dist         | 从多边形边界扩展ROI的距离。                 |0.0 米   |

基于CNN的障碍物分割
------------------------------------------------
高精地图 ROI过滤之后，Apollo得到已过滤、只包含属于ROI内的点云，大部分背景障碍物，如路侧的建筑物、树木等均被移除，ROI内的点云被传递到分割模块。分割模块检测和划分前景障碍物，例如汽车，卡车，自行车和行人。

  |输入                                                                        |输出                             |
  |----------------------------------------------------------------------------|---------------------------------------------------------------|
  |点云（3D数据集）                                         |对应于ROI中的障碍物对象数据集    |
  |表示在HDMap中定义的ROI内的点的点索引       |                               |                                                                              
Apollo 使用深度卷积神经网络提高障碍物识别与分割的精度，障碍物分割包含以下四步：
- 通道特征提取
- 基于卷积神经网络的障碍物预测
- 障碍物集群
- 后期处理

卷积神经网络详细介绍如下：

### 通道特征提取

给定一个点云框架，Apollo在地方坐标系中构建俯视图（即投影到X-Y平面）2D网格。 基于点的X、Y坐标，相对于LiDAR传感器原点的预定范围内，每个点被量化为2D网格的一个单元。 量化后，Apollo计算网格内每个单元格中点的8个统计测量，这将是下一步中传递给CNN的输入通道特征。 

计算的8个统计测量：

1. 单元格中点的最大高度
2. 单元格中最高点的强度
3. 单元格中点的平均高度
4. 单元格中点的平均强度
5. 单元格中的点数
6. 单元格中心相对于原点的角度
7. 单元格中心与原点之间的距离
8. 二进制值标示单元格是空还是被占用

### 基于卷积神经网络的障碍物预测

基于上述通道特征，Apollo使用深度完全卷积神经网络（FCNN）来预测单元格障碍物属性，包括潜在物体中心的偏移位移（称为中心偏移）、对象性
积极性和物体高度。如图2所示，网络的输入为 *W* x *H* x *C* 通道图像，其中：

- *W* 代表网格中的列数
- *H* 代表网格中的行数
- *C* 代表通道特征数

完全卷积神经网络由三层构成：
- 下游编码层（特征编码器）
- 上游解码层（特征解码器）
- 障碍物属性预测层（预测器）

特征编码器将通道特征图像作为输入，并且随着特征抽取的增加而连续**下采样**其空间分辨率。 然后特征解码器逐渐对特征图像 **上采样**到输入2D网格的空间分辨率，可以恢复特征图像的空间细节，以促进单元格方向的障碍物位置、速度属性预测。 根据具有非线性激活（即ReLu）层的堆叠卷积/分散层来实现 **下采样**和 **上采样**操作。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/FCNN.png" width="99%"></div>

<div align=center>图 2 FCNN在单元格方向上的障碍物预测</div>

### 障碍物聚类
在基于CNN的预测之后，Apollo获取单个单元格的预测信息。利用四个单元对象属性图像，其中包含：

- 中心偏移
- 对象性
- 积极性
- 对象高度

为生成障碍物，Apollo基于单元格中心偏移，预测构建有向图，并搜索连接的组件作为候选对象集群。

如图3所示，每个单元格是图的一个节点，并且基于单元格的中心偏移预测构建有向边，其指向对应于另一单元的父节点。

如图3，Apollo采用压缩的联合查找算法（Union Find algorithm ）有效查找连接组件，每个组件都是候选障碍物对象集群。对象是单个单元格成为有效对象的概率。因此，Apollo将非对象单元定义为目标小于0.5的单元格。因此，Apollo过滤出每个候选对象集群的空单元格和非对象集。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/obstacle_clustering.png" width="99%"></div>

<div align=center>图 3 障碍聚类</div>

(a) 红色箭头表示每个单元格对象中心偏移预测；蓝色填充对应于物体概率不小于0.5的对象单元。

(b) 固体红色多边形内的单元格组成候选对象集群。

由五角星填充的红色范围表示对应于连接组件子图的根节点（单元格）。 

一个候选对象集群可以由其根节点彼此相邻的多个相邻连接组件组成。

### 后期处理

聚类后，Apollo获得一组候选对象集，每个候选对象集包括若干单元格。 

在后期处理中，Apollo首先对所涉及的单元格的积极性和物体高度值，平均计算每个候选群体的检测置信度分数和物体高度。 然后，Apollo去除相对于预测物体高度太高的点，并收集每个候选集中的有效单元格的点。 最后，Apollo删除具有非常低的可信度分数或小点数的候选聚类，以输出最终的障碍物集/分段。

用户定义的参数可以在`modules/perception/model/cnn_segmentation/cnnseg.conf`的配置文件中设置。 下表说明了CNN细分的参数用法和默认值：


 |参数名称             |使用说明                                           |默认值    |
 |-----------------------------------|--------------------------------------------------------------------------------------------|-----------|
 |objectness_thresh                  |用于在障碍物聚类步骤中过滤掉非对象单元的对象的阈值。 |0.5        |
 |use_all_grids_for_clustering       |指定是否使用所有单元格在障碍物聚类步骤中构建图形的选项。如果不是，则仅考虑占用的单元格。   |true   |
 |confidence_thresh                  |用于在后期处理过程中滤出候选聚类的检测置信度得分阈值。    |0.1    |
 |height_thresh                      |如果是非负数，则在后处理步骤中将过滤掉高于预测物体高度的点。 |0.5 meters |
 |min_pts_num                        |在后期处理中，删除具有小于min_pts_num点的候选集群。 |3   |
 |use_full_cloud                     |如果设置为true，则原始点云的所有点将用于提取通道特征。 否则仅使用输入点云的点（即，HDMap ROI过滤器之后的点）。  |true |
 |gpu_id                             |在基于CNN的障碍物预测步骤中使用的GPU设备的ID。            |0          |
 |feature_param {width}              |2D网格的X轴上的单元格数。                      |512        |
 |feature_param {height}             |2D网格的Y轴上的单元格数。                     |512        |
 |feature_param {range}              |2D格栅相对于原点（LiDAR传感器）的范围。             |60 meters  |

**注意：提供的模型是一个样例，仅限于实验所用。**

MinBox 障碍物边框构建
--------------

对象构建器组件为检测到的障碍物建立一个边界框。因为LiDAR传感器的遮挡或距离，形成障碍物的点云可以是稀疏的，并且仅覆盖一部分表面。因此，盒构建器将恢复给定多边形点的完整边界框。即使点云稀疏，边界框的主要目的还是预估障碍物（例如，车辆）的方向。同样地，边框也用于可视化障碍物。

算法背后的想法是找到给定多边形点边缘的所有区域。在以下示例中，如果AB是边缘，则Apollo将其他多边形点投影到AB上，并建立具有最大距离的交点对，这是属于边框的边缘之一。然后直接获得边界框的另一边。通过迭代多边形中的所有边，在以下图4所示，Apollo确定了一个6边界边框，将选择具有最小面积的方案作为最终的边界框。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/object_building.png"></div>

<div align=center>图 4 MinBox 对象构建</div>

HM对象跟踪
-----------------

HM对象跟踪器跟踪分段检测到的障碍物。通常，它通过将当前检测与现有跟踪列表相关联，来形成和更新跟踪列表，如不再存在，则删除旧的跟踪列表，并在识别出新的检测时生成新的跟踪列表。 更新后的跟踪列表的运动状态将在关联后进行估计。 在HM对象跟踪器中，**匈牙利算法**(Hungarian algorithm)用于检测到跟踪关联，并采用 **鲁棒卡尔曼滤波器**(Robust Kalman Filter) 进行运动估计。

### 检测跟踪关联（Detection-to-Track Association）

当将检测与现有跟踪列表相关联时，Apollo构建了一个二分图，然后使用 **匈牙利算法**以最小成本（距离）找到最佳检测跟踪匹配。

**计算关联距离矩阵**

首先，建立一个关联距离矩阵。根据一系列关联特征（包括运动一致性，外观一致性等）计算给定检测和一条轨迹之间的距离。HM跟踪器距离计算中使用的一些特征如下所示：

  |关联特征名称 |描述                       |
  |-------------------------|----------------------------------|
  |location_distance        |评估运动一致性                      |
  |direction_distance       |评估运动一致性                       |
  |bbox_size_distance       |评估外观一致性 |
  |point_num_distance       |评估外观一致性 |
  |histogram_distance       |评估外观一致性 |

此外，还有一些重要的距离权重参数，用于将上述关联特征组合成最终距离测量。

**匈牙利算法的二分图匹配**

给定关联距离矩阵，如图5所示，Apollo构造了一个二分图，并使用 **匈牙利算法**通过最小化距离成本找到最佳的检测跟踪匹配。它解决了O(n\^3)时间复杂度中的赋值问题。 为了提高其计算性能，通过删除距离大于合理的最大距离阈值的顶点，将原始的二分图切割成子图后实现了匈牙利算法。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/bipartite_graph_matching.png"></div>

<div align=center>图 5 二分图匹配（Bipartite Graph Matching）</div>

### 跟踪动态预估 （Track Motion Estimation）

在检测到跟踪关联之后，HM对象跟踪器使用 **鲁棒卡尔曼滤波器**来利用恒定速度运动模型估计当前跟踪列表的运动状态。 运动状态包括锚点和速度，分别对应于3D位置及其3D速度。 为了克服由不完美的检测引起的可能的分心，在跟踪器的滤波算法中实现了鲁棒统计技术。

**观察冗余**

在一系列重复观测中选择速度测量，即滤波算法的输入，包括锚点移位、边界框中心偏移、边界框角点移位等。冗余观测将为滤波测量带来额外的鲁棒性， 因为所有观察失败的概率远远小于单次观察失败的概率。

**分解**

高斯滤波算法 （Gaussian Filter algorithms）总是假设它们的高斯分布产生噪声。 然而，这种假设可能在运动预估问题中失败，因为其测量的噪声可能来自直方分布。 为了克服更新增益的过度估计，在过滤过程中使用故障阈值。

**更新关联质量**

原始卡尔曼滤波器更新其状态不区分其测量的质量。 然而，质量是滤波噪声的有益提示，可以估计。 例如，在关联步骤中计算的距离可以是一个合理的测量质量估计。 根据关联质量更新过滤算法的状态，增强了运动估计问题的鲁棒性和平滑度。

HM对象跟踪器的高级工作流程如图6所示。

<div align=center><img src="https://raw.githubusercontent.com/ApolloAuto/apollo/master/docs/specs/images/3d_obstacle_perception/hm_object_tracker.png"></div>

<div align=center>图 6 HM对象跟踪器工作流</div>

1）构造跟踪对象并将其转换为世界坐标。

2）预测现有跟踪列表的状态，并对其匹配检测。

3）在更新后的跟踪列表中更新运动状态，并收集跟踪结果。

## 参考
- [匈牙利算法](https://zh.wikipedia.org/zh-cn/%E5%8C%88%E7%89%99%E5%88%A9%E7%AE%97%E6%B3%95)
- [地方坐标系](https://baike.baidu.com/item/%E5%9C%B0%E6%96%B9%E5%9D%90%E6%A0%87%E7%B3%BB/5154246)
- [Fully Convolutional Networks for Semantic Segmentation](https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf)



# ==============================
# Planning模块架构和概述

## 数据输入和输出

### 输出数据

Planning模块的输出数据类型定义在`planning.proto`，如下图所示：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image001.png)

#### *planning.proto*

在proto数据的定义中，输出数据包括总时间、总长度和确切的路径信息，输出数据由控制单元解析执行，输出数据结构定义在`repeated apollo.common.TrajectoryPointtrajectory_point`。

`trajectory point`类继承自`path_point`类，并新增了speed、acceleration和timing属性。
定义在`pnc_point.proto`中的`trajectory_point`包含了路径的详细属性。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image002.png)

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image003.png)

除了路径信息，Planning模块输出了多种注释信息。主要的注释数据包括：

- Estop
- DecisionResult
- 调试信息

`Estop`是标示了错误和异常的指令。例如，当自动驾驶的车辆碰到了障碍物或者无法遵守交通规则时将发送estop信号。`DecisionResult`主要用于展示模拟的输出结果以方便开发者更好的了解Planning模块的计算结果。更多详细的中间值结果会被保存并输出作为调试信息供后续的调试使用。

## 输入数据

为了计算最终的输出路径，Planning模块需要统一的规划多个输入数据。Planning模块的输入数据包括：

- Routing
- 感知和预测
- 车辆状态和定位
- 高清地图

Routing定义了概念性问题“我想去哪儿”，消息定义在`routing.proto`文件中。`RoutingResponse`包含了`RoadSegment`，`RoadSegment`指明了车辆到达目的地应该遵循的路线。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image004.png)

关于概念性问题“我周围有什么”的消息定义在`perception_obstacles.proto`和`traffic_light_detection.proto`中。`perception_obstacles.proto`定义了表示车辆周围的障碍物的数据，车辆周围障碍物的数据由感知模块提供。`traffic_light_detection`定义了信号灯状态的数据。除了已被感知的障碍物外，动态障碍物的路径预测对Planning模块也是非常重要的数据，因此`prediction.proto`封装了`perception_obstacle`消息来表示预测路径。请参考下述图片：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image005.png)

每个预测的路径都有其单独的可能性，而且每个动态障碍物可能有多个预测路径。

除了概念性问题“我想去哪儿”和“我周围有什么”，另外一个重要的概念性问题是“我在哪”。关于该问题的数据通过高清地图和定位模块获得。定位信息和车辆车架信息被封装在`VehicleState`消息中，该消息定义在`vehicle_state.proto`，参考下述图片：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image009.png)

## 代码结构和类层次

代码组织方式如下图所示：Planning模块的入口是`planning.cc`。在Planning模块内部，重要的类在下图中展示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image006.png)

`ReferenceLineInfo`对`ReferenceLine`类进行了封装，为Planning模块提供了平滑的指令执行序列。
**Frame**包含了所有的数据依赖关系，例如包含了预测路径信息的障碍物，自动驾驶车辆的状态等。
**HD-Ma**p在Planning模块内作为封装了多个数据的库使用，提供不同特点的地图数据查询需求。
**EM Planne**r执行具体的Planning任务，继承自**Planner**类。Apollo2.0中的**EM Planner**类和之前发布的**RTK Planner**类都继承自Planner类。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image007.png)

例如，在EM Planner执行的一次planning循环的内部，采用迭代执行的方法，tasks的三个类别交替执行。“**决策/优化**”类的关系在下述图片中展示：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/class_architecture_planning/image008.png)

- **Deciders** 包括 traffic decider, path decider and speed decider.

- **Path Optimizers** 为DP/QP path optimizers.

- **Speed Optimizers** 为DP/QP speed optimizers.

| **附注：**                                |
| ---------------------------------------- |
| DP表示动态规划（dynamic programming），QP表示二次规划（quadratic programming）。经过计算步骤后，最终的路径数据经过处理后传递到下一个节点模块进行路径的执行。 |



# =====================
# 二次规划（QP）样条路径优化

_**Tip**: 为了更好的展示本文档中的等式，我们建议使用者使用带有[插件](https://chrome.google.com/webstore/detail/tex-all-the-things/cbimabofgmfdkicghcadidpemeenbffn)的Chrome浏览器，或者将Latex等式拷贝到[在线编辑公式网站](http://www.hostmath.com/)进行浏览。_

二次规划（QP）+样条插值

## 1.  目标函数

### 1.1  获得路径长度

路径定义在station-lateral坐标系中。**s**的变化区间为从车辆当前位置点到默认路径的长度。

### 1.2   获得样条段

将路径划分为**n**段，每段路径用一个多项式来表示。

### 1.3  定义样条段函数

每个样条段 ***i*** 都有沿着参考线的累加距离$d_i$。每段的路径默认用5介多项式表示。

<p>
$$
l = f_i(s)
  = a_{i0} + a_{i1} \cdot s + a_{i2} \cdot s^2 + a_{i3} \cdot s^3 + a_{i4} \cdot s^4 + a_{i5} \cdot s^5        (0 \leq s \leq d_{i})
$$
</p>

l=fi(s)=ai0+ai1⋅s+ai2⋅s2+ai3⋅s3+ai4⋅s4+ai5⋅s5(0≤s≤di)

### 1.4  定义每个样条段优化目标函数

<p>
$$
cost = \sum_{i=1}^{n} \Big( w_1 \cdot \int\limits_{0}^{d_i} (f_i')^2(s) ds + w_2 \cdot \int\limits_{0}^{d_i} (f_i'')^2(s) ds + w_3 \cdot \int\limits_{0}^{d_i} (f_i^{\prime\prime\prime})^2(s) ds \Big)
$$
</p>

### 1.5  将开销（cost）函数转换为QP公式

QP公式:
<p>
$$
\begin{aligned}
minimize  & \frac{1}{2}  \cdot x^T \cdot H \cdot x  + f^T \cdot x \\
s.t. \qquad & LB \leq x \leq UB \\
      & A_{eq}x = b_{eq} \\
      & Ax \geq b
\end{aligned}
$$
</p>
下面是将开销（cost）函数转换为QP公式的例子：
<p>
$$
f_i(s) ＝
\begin{vmatrix} 1 & s & s^2 & s^3 & s^4 & s^5 \end{vmatrix}
\cdot
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix}   
$$
</p>

且
<p>
$$
f_i'(s) =
\begin{vmatrix} 0 & 1 & 2s & 3s^2 & 4s^3 & 5s^4 \end{vmatrix}
\cdot
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix}   
$$
</p>


且
<p>
$$
f_i'(s)^2 =
\begin{vmatrix} a_{i0} & a_{i1} & a_{i2} & a_{i3} & a_{i4} & a_{i5}  \end{vmatrix} 
\cdot 
\begin{vmatrix} 0 \\ 1 \\ 2s \\ 3s^2 \\ 4s^3 \\ 5s^4 \end{vmatrix} 
\cdot 
\begin{vmatrix} 0 & 1 & 2s & 3s^2 & 4s^3 & 5s^4 \end{vmatrix} 
\cdot 
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}  \end{vmatrix}
$$
</p>
然后得到，
<p>
$$
\int\limits_{0}^{d_i} f_i'(s)^2 ds ＝
\int\limits_{0}^{d_i}
\begin{vmatrix} a_{i0} & a_{i1} & a_{i2} & a_{i3} & a_{i4} & a_{i5} \end{vmatrix} 
\cdot  
\begin{vmatrix} 0 \\ 1 \\ 2s \\ 3s^2 \\ 4s^3 \\ 5s^4 \end{vmatrix} 
\cdot 
\begin{vmatrix} 0 & 1 & 2s & 3s^2 & 4s^3 & 5s^4 \end{vmatrix} 
\cdot 
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}  \end{vmatrix} ds
$$
</p>


从聚合函数中提取出常量得到，
<p>
$$
\int\limits_{0}^{d_i} f'(s)^2 ds ＝
\begin{vmatrix} a_{i0} & a_{i1} & a_{i2} & a_{i3} & a_{i4} & a_{i5} \end{vmatrix} 
\cdot 
\int\limits_{0}^{d_i}  
\begin{vmatrix} 0 \\ 1 \\ 2s \\ 3s^2 \\ 4s^3 \\ 5s^4 \end{vmatrix} 
\cdot 
\begin{vmatrix} 0 & 1 & 2s & 3s^2 & 4s^3 & 5s^4 \end{vmatrix} ds 
\cdot 
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}  \end{vmatrix}
$$
$$
＝\begin{vmatrix} a_{i0} & a_{i1} & a_{i2} & a_{i3} & a_{i4} & a_{i5} \end{vmatrix} 
\cdot \int\limits_{0}^{d_i}
\begin{vmatrix} 
0  & 0 &0&0&0&0\\ 
0 & 1 & 2s & 3s^2 & 4s^3 & 5s^4\\
0 & 2s & 4s^2 & 6s^3 & 8s^4 & 10s^5\\
0 & 3s^2 &  6s^3 & 9s^4 & 12s^5&15s^6 \\
0 & 4s^3 & 8s^4 &12s^5 &16s^6&20s^7 \\
0 & 5s^4 & 10s^5 & 15s^6 & 20s^7 & 25s^8 
\end{vmatrix} ds 
\cdot 
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix}
$$
</p>

最后得到，

<p>
$$
\int\limits_{0}^{d_i} 
f'_i(s)^2 ds =\begin{vmatrix} a_{i0} & a_{i1} & a_{i2} & a_{i3} & a_{i4} & a_{i5} \end{vmatrix} 
\cdot \begin{vmatrix} 
0 & 0 & 0 & 0 &0&0\\ 
0 & d_i & d_i^2 & d_i^3 & d_i^4&d_i^5\\
0& d_i^2 & \frac{4}{3}d_i^3& \frac{6}{4}d_i^4 & \frac{8}{5}d_i^5&\frac{10}{6}d_i^6\\
0& d_i^3 & \frac{6}{4}d_i^4 & \frac{9}{5}d_i^5 & \frac{12}{6}d_i^6&\frac{15}{7}d_i^7\\
0& d_i^4 & \frac{8}{5}d_i^5 & \frac{12}{6}d_i^6 & \frac{16}{7}d_i^7&\frac{20}{8}d_i^8\\
0& d_i^5 & \frac{10}{6}d_i^6 & \frac{15}{7}d_i^7 & \frac{20}{8}d_i^8&\frac{25}{9}d_i^9
\end{vmatrix} 
\cdot 
\begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix}
$$
</p>

请注意我们最后得到一个6介的矩阵来表示5介样条插值的衍生开销。
应用同样的推理方法可以得到2介，3介样条插值的衍生开销。

## 2  约束条件  

### 2.1  初始点约束

假设第一个点为 ($s_0$, $l_0$), ($s_0$, $l'_0$) and ($s_0$, $l''_0$)，其中$l_0$ , $l'_0$ and $l''_0$表示横向的偏移，并且规划路径的起始点的第一，第二个点的衍生开销可以从$f_i(s)$, $f'_i(s)$, $f_i(s)''$计算得到。

将上述约束转换为QP约束等式，使用等式：

<p>
$$
A_{eq}x = b_{eq}
$$
</p>

下面是转换的具体步骤：

<p>
$$
f_i(s_0) = 
\begin{vmatrix} 1 & s_0 & s_0^2 & s_0^3 & s_0^4&s_0^5 \end{vmatrix} 
\cdot 
\begin{vmatrix}  a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}\end{vmatrix} = l_0
$$
</p>
且
<p>
$$
f'_i(s_0) = 
\begin{vmatrix} 0& 1 & 2s_0 & 3s_0^2 & 4s_0^3 &5 s_0^4 \end{vmatrix} 
\cdot 
\begin{vmatrix}  a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix} = l'_0
$$
</p>
且 
<p>
$$
f''_i(s_0) = 
\begin{vmatrix} 0&0& 2 & 3\times2s_0 & 4\times3s_0^2 & 5\times4s_0^3  \end{vmatrix} 
\cdot 
\begin{vmatrix}  a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix} = l''_0
$$
</p>
其中，i是包含$s_0$的样条段的索引值。

### 2.2  终点约束

和起始点相同，终点$(s_e, l_e)$ 也应当按照起始点的计算方法生成约束条件。

将起始点和终点组合在一起，得出约束等式为：

<p>
$$
\begin{vmatrix} 
 1 & s_0 & s_0^2 & s_0^3 & s_0^4&s_0^5 \\
 0&1 & 2s_0 & 3s_0^2 & 4s_0^3 & 5s_0^4 \\
 0& 0&2 & 3\times2s_0 & 4\times3s_0^2 & 5\times4s_0^3  \\
 1 & s_e & s_e^2 & s_e^3 & s_e^4&s_e^5 \\
 0&1 & 2s_e & 3s_e^2 & 4s_e^3 & 5s_e^4 \\
 0& 0&2 & 3\times2s_e & 4\times3s_e^2 & 5\times4s_e^3  
 \end{vmatrix} 
 \cdot 
 \begin{vmatrix}  a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5} \end{vmatrix} 
 = 
 \begin{vmatrix}
 l_0\\
 l'_0\\
 l''_0\\
 l_e\\
 l'_e\\
 l''_e\\
 \end{vmatrix}
$$
</p>

### 2.3  平滑节点约束

该约束的目的是使样条的节点更加平滑。假设两个段$seg_k$ 和$seg_{k+1}$互相连接，且$seg_k$的累计值s为$s_k$。计算约束的等式为：

<p>
$$
f_k(s_k) = f_{k+1} (s_0)
$$
</p>
下面是计算的具体步骤：
<p>
$$
\begin{vmatrix} 
 1 & s_k & s_k^2 & s_k^3 & s_k^4&s_k^5 \\
 \end{vmatrix} 
 \cdot 
 \begin{vmatrix} 
 a_{k0} \\ a_{k1} \\ a_{k2} \\ a_{k3} \\ a_{k4} \\ a_{k5} 
 \end{vmatrix} 
 = 
\begin{vmatrix} 
 1 & s_{0} & s_{0}^2 & s_{0}^3 & s_{0}^4&s_{0}^5 \\
 \end{vmatrix} 
 \cdot 
 \begin{vmatrix} 
 a_{k+1,0} \\ a_{k+1,1} \\ a_{k+1,2} \\ a_{k+1,3} \\ a_{k+1,4} \\ a_{k+1,5} 
 \end{vmatrix}
$$
</p>
然后
<p>
$$
\begin{vmatrix} 
 1 & s_k & s_k^2 & s_k^3 & s_k^4&s_k^5 &  -1 & -s_{0} & -s_{0}^2 & -s_{0}^3 & -s_{0}^4&-s_{0}^5\\
 \end{vmatrix} 
 \cdot 
 \begin{vmatrix} 
 a_{k0} \\ a_{k1} \\ a_{k2} \\ a_{k3} \\ a_{k4} \\ a_{k5} \\ a_{k+1,0} \\ a_{k+1,1} \\ a_{k+1,2} \\ a_{k+1,3} \\ a_{k+1,4} \\ a_{k+1,5}  
 \end{vmatrix} 
 = 0
$$
</p>
将$s_0$ = 0代入等式。

同样地，可以为下述等式计算约束等式：
<p>
$$
f'_k(s_k) = f'_{k+1} (s_0)
\\
f''_k(s_k) = f''_{k+1} (s_0)
\\
f'''_k(s_k) = f'''_{k+1} (s_0)
$$
</p>

### 2.4  点采样边界约束

在路径上均匀的取样**m**个点，检查这些点上的障碍物边界。将这些约束转换为QP约束不等式，使用不等式：

<p>
$$
Ax \geq b
$$
</p>

首先基于道路宽度和周围的障碍物找到点 $(s_j, l_j)$的下边界$l_{lb,j}$，且$j\in[0, m]$。计算约束的不等式为：

<p>
$$
\begin{vmatrix} 
 1 & s_0 & s_0^2 & s_0^3 & s_0^4&s_0^5 \\
  1 & s_1 & s_1^2 & s_1^3 & s_1^4&s_1^5 \\
 ...&...&...&...&...&... \\
 1 & s_m & s_m^2 & s_m^3 & s_m^4&s_m^5 \\
 \end{vmatrix} \cdot \begin{vmatrix}a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}  \end{vmatrix} 
 \geq 
 \begin{vmatrix}
 l_{lb,0}\\
 l_{lb,1}\\
 ...\\
 l_{lb,m}\\
 \end{vmatrix}
$$
</p>


同样地，对上边界$l_{ub,j}$，计算约束的不等式为：
<p>
$$
\begin{vmatrix} 
 -1 & -s_0 & -s_0^2 & -s_0^3 & -s_0^4&-s_0^5 \\
  -1 & -s_1 & -s_1^2 & -s_1^3 & -s_1^4&-s_1^5 \\
 ...&...-&...&...&...&... \\
 -1 & -s_m & -s_m^2 & -s_m^3 & -s_m^4&-s_m^5 \\
 \end{vmatrix} 
 \cdot 
 \begin{vmatrix} a_{i0} \\ a_{i1} \\ a_{i2} \\ a_{i3} \\ a_{i4} \\ a_{i5}  \end{vmatrix} 
 \geq
 -1 \cdot
 \begin{vmatrix}
 l_{ub,0}\\
 l_{ub,1}\\
 ...\\
 l_{ub,m}\\
 \end{vmatrix}
$$
</p>




# ======================
# Apollo 3.0传感器安装指南

## 需要的硬件

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_required_hardware.png)

外部设备

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_peripherals.png)

## 坐标系

单位：毫米（mm）

原点：车辆后轮轴中心

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure1.png)

**Figure 1. 原点和坐标系**

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure2.png)

**Figure 2. 卡车坐标系和安装摄像机与雷达的示意图**

## 传感器安装指南
###	IMU/GPS
IMU/GPS需要安装在靠近后车轮毂的位置。GPS天线需要安装在车辆顶部。
###	Radar
远程雷达需要安装在车辆前保险杠上，请参考Figure 1 and Figure 2展示的信息。
###	Camera
一个6mm镜头的摄像机应该面向车辆的前方。前向摄像机应当安装在车辆前部的中心位置，离地面高度为1600mm到2000mm（Camera 1），或者安装在车辆挡风玻璃上（Camera 2）。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure3.png)

**Figure 3. 安装摄像机的示例图**

摄像机安装完成后，摄像机w、r、t的物理坐标x、y、z应该被记录在校准文件里。

#### 安装摄像机后的检验

三个摄像机的方位应当全部设置为0。摄像机安装后，需要车辆在公路以直线开动一段距离并记录一个rosbag，通过rosbag的回放，摄像机的方位需要重新调整以设置间距、偏航角并将角度转置为0度。如果摄像机被正确的安装，地平线应该在画面高度方向上的正中间并且不倾斜。灭点同样应该在画面的正中间。请参考下述图片以将摄像机设置为最佳状态：

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/perception_setup_figure4.png)

**Figure 4. 摄像机安装后的画面示例。地平线应该在画面高度方向上的正中间并且不倾斜。灭点同样应该在画面的正中间。 红色线段显示了画面高度和宽度方向上的中点。**

估测的平移参数的示例如下所示：
```
header:
    seq: 0
    stamp:
        secs: 0
        nsecs: 0
    frame_id: white_mkz
child_frame_id: onsemi_obstacle
transform:
    rotation:
        x:  0.5
        y: -0.5
        z:  0.5
        w: -0.5
    translation:	
        x: 1.895
        y: -0.235
        z: 1.256 
```
如果角度不为0，则上述数据需要重新校准并在四元数中表示（参考上例中的transform->rotation	）


# ===================
# Apollo坐标系统

我们欢迎每一位开发者加入Apollo开发平台。Apollo系统涉及到了多种坐标系。在本文档中，我们将讨论在Apollo系统中使用的各个坐标系的定义。

## 1. 全球地理坐标系统

在Apollo系统中，我们采用全球地理坐标系统来表示高精地图（HD Map）中各个元素的地理位置。全球地理坐标系统的通常用途是用来表示纬度、经度和海拔。Apollo采用的是WGS84（World Geodetic System 1984）作为标准坐标系来表示物体的纬度和经度。通过使用该标准坐标系统，我们可以使用2个数字：x坐标和y坐标来唯一的确定地球表面上除北极点之外的所有点，其中x坐标表示经度，y坐标表示纬度。WGS-84常用于GIS服务，例如地图绘制、定位和导航等。全球地理坐标系统的定义在下图中展示。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/coordination_01.png)

## 2. 局部坐标系 – 东-北-上（East-North-Up ENU）

在Apollo系统中，局部坐标系的定义为：

z轴 – 指向上方（和重力线成一条直线）

y轴 – 指向北面

x轴 – 指向东面

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/coordination_02.png)

ENU局部坐标系依赖于在地球表面上建立的3D笛卡尔坐标系。
通用横轴墨卡托正形投影（Universal Transverse Mercator  UTM）使用2D的笛卡尔坐标系来给出地球表面点的位置。这不仅只是一次地图的映射。该坐标系统将地球划分为60个区域，每个区域表示为6度的经度带，并且在每个区域上使用割线横轴墨卡托投影。在Apollo系统中，UTM坐标系统在定位、Planning等模块中作为局部坐标系使用。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/coordination_03.png)

关于UTM坐标系统的使用，我们遵从国际标准规范。开发者可以参考下述网站获取更多细节：

[http://geokov.com/education/utm.aspx](http://geokov.com/education/utm.aspx)

[https://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system](https://en.wikipedia.org/wiki/Universal_Transverse_Mercator_coordinate_system)

## 3. 车辆坐标系 – 右-前-上（Right-Forward-Up RFU）

车辆坐标系的定义为：

z轴 – 通过车顶垂直于地面指向上方

y轴 – 在行驶的方向上指向车辆前方

x轴 – 面向前方时，指向车辆右侧

车辆坐标系的原点在车辆后轮轴的中心。

![Image](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/coordination_04.png)

# ==============================================
# DreamView用法介绍

DreamView是一个web应用程序，提供如下的功能：
1. 可视化显示当前自动驾驶车辆模块的输出信息，例如规划路径、车辆定位、车架信息等。
2. 为使用者提供人机交互接口以监测车辆硬件状态，对模块进行开关操作，启动自动驾驶车辆等。
3. 提供调试工具，例如PnC监视器可以高效的跟踪模块输出的问题

## 界面布局和特性

该应用程序的界面被划分为多个区域：标题、侧边栏、主视图和工具视图。

### 标题
标题包含4个下拉列表，可以像下述图片所示进行操作：
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/header.png) 

附注：导航模块是在Apollo 2.5版本引入的满足低成本测试的特性。在该模式下，Baidu或Google地图展现的是车辆的绝对位置，而主视图中展现的是车辆的相对位置。

### 侧边栏和工具视图
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/sidebar.png) 
侧边栏控制着显示在工具视图中的模块

### Tasks
在DreamView中使用者可以操作的tasks有：
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/tasks.png)

* **Quick Start**: 当前选择的模式支持的指令。通常情况下，

    **setup**: 开启所有模块

    **reset all**: 关闭所有模块

    **start auto**: 开始车辆的自动驾驶
* **Others**: 工具经常使用的开关和按钮
* **Module Delay**: 从模块中输出的两次事件的时间延迟
* **Console**: 从Apollo平台输出的监视器信息

### Module Controller
监视硬件状态和对模块进行开关操作
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/module_controller.png) 

### Layer Menu
显式控制各个元素是否显示的开关
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/layer_menu.png) 

### Route Editing
在向Routing模块发送寻路信息请求前可以编辑路径信息的可视化工具
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/route_editing.png)

### Data Recorder
将问题报告给rosbag中的drive event的界面
![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/data_recorder.png)  

### Default Routing
预先定义的路径或者路径点，该路径点称为兴趣点（POI）。

![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/default_routing.png) 

如果打开了路径编辑模式，路径点可被显式的在地图上添加。

如果关闭了路径编辑模式，点击一个期望的POI会向服务器发送一次寻路请求。如果只选择了一个点，则寻路请求的起点是自动驾驶车辆的当前点。否则寻路请求的起点是选择路径点中的第一个点。

查看Map目录下的[default_end_way_point.txt](https://github.com/ApolloAuto/apollo/blob/master/modules/map/data/demo/default_end_way_point.txt)文件可以编译POI信息。例如，如果选择的地图模式为“Demo”，则在`modules/map/data/demo`目录下可以查看对应的 [default_end_way_point.txt](https://github.com/ApolloAuto/apollo/blob/master/modules/map/data/demo/default_end_way_point.txt) 文件。

### 主视图
主视图在web页面中以动画的方式展示3D计算机图形

![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/mainview.png) 

下表列举了主视图中各个元素：

| Visual Element                           | Depiction Explanation                    |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image002.png) | <ul><li>自动驾驶车辆    </li></ul>                  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image004.png) | <ul><li>车轮转动的比率</li> <li>左右转向灯的状态</li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image003.png) | <ul><li>交通信号灯状态</li></ul>          |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image005.png) |<ul><li>  驾驶状态（AUTO/DISENGAGED/MANUAL等） </li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image006.png) | <ul><li>行驶速度 km/h</li> <li>加速速率/刹车速率</li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image026.png) | <ul><li> 红色粗线条表示建议的寻路路径</li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image038.png) |<ul><li>  轻微移动物体决策—橙色表示应该避开的区域 </li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image062.png) |<ul><li>  绿色的粗曲线条带表示规划的轨迹 </li></ul> |

#### 障碍物

| Visual Element                           | Depiction Explanation                    |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image010.png) | <ul><li>车辆障碍物   </li></ul>                     |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image012.png) | <ul><li>行人障碍物    </li></ul>                 |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image014.png) | <ul><li>自行车障碍物      </li></ul>                |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image016.png) | <ul><li>未知障碍物 </li></ul>                        |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image018.png) | <ul><li>速度方向显示了移动物体的方向，长度随速度按照比率变化</li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image020.png) | <ul><li>白色箭头显示了障碍物的移动方向</li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image022.png) | 黄色文字表示: <ul><li>障碍物的跟踪ID</li><li>自动驾驶车辆和障碍物的距离及障碍物速度</li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image024.png) | <ul><li>线条显示了障碍物的预测移动轨迹，线条标记为和障碍物同一个颜色</li></ul>  |

#### Planning决策
##### 决策栅栏区

决策栅栏区显示了Planning模块对车辆障碍物做出的决策。每种类型的决策会表示为不同的颜色和图标，如下图所示：

| Visual Element                           | Depiction Explanation                    |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image028.png) | <ul><li>**停止** 表示物体主要的停止原因</li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image030.png) | <ul><li>**停止** 表示物体的停止原因n</li></ul>  |
| ![2](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image032.png) | <ul><li>**跟车** 物体</li></ul>                        |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image034.png) | <ul><li>**让行** 物体决策—点状的线条连接了各个物体</li></ul>  |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image036.png) | <ul><li>**超车** 物体决策—点状的线条连接了各个物体</li></ul>  |

线路变更是一个特殊的决策，因此不显示决策栅栏区，而是将路线变更的图标显示在车辆上。

| Visual Element                           | Depiction Explanation                    |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/change-lane-left.png) | <ul><li>变更到**左**车道 </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/change-lane-right.png) | <ul><li>变更到**右**车道 </li></ul>|

在优先通行的规则下，当在交叉路口的停车标志处做出让行决策时，被让行的物体在头顶会显示让行图标

| Visual Element                                       | Depiction Explanation          |
| ---------------------------------------------------- | ------------------------------ |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image037.png) | 停止标志处的让行物体 |

##### 停止原因

如果显示了停止决策栅栏区，则停止原因展示在停止图标的右侧。可能的停止原因和对应的图标为：

| Visual Element                           | Depiction Explanation                    |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image040.png) | <ul><li>**前方道路侧边区域** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image042.png) | <ul><li>**前方人行道** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image044.png) | <ul><li>**到达目的地** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image046.png) | <ul><li>**紧急停车**  </li></ul>       |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image048.png) | <ul><li> **自动驾驶模式未准备好** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image050.png) | <ul><li>**障碍物阻塞道路**</li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image052.png) | <ul><li> **前方行人穿越** </li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image054.png) | <ul><li>**黄/红信号灯** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image056.png) | <ul><li> **前方有车辆** </li></ul> |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image058.png) | <ul><li> **前方停止标志** </li></ul>|
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/0clip_image060.png) | <ul><li>**前方让行标志** </li></ul> |

#### 视图
可以在主视图中展示多种从**Layer Menu**选择的视图模式：

| Visual Element                           | Point of View                            |
| ---------------------------------------- | ---------------------------------------- |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/default_view.png) | <ul><li>**默认视图**      </li></ul> |       |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/near_view.png) | <ul><li>**近距离视图**   </li></ul> |             |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/overhead_view.png) | <ul><li>**俯瞰视图**    </li></ul> |        |
| ![](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/images/dreamview_usage_table/map_view.png) | **地图** <ul><li> 放大/缩小：滚动鼠标滚轮或使用两根手指滑动 </li><li> 移动：按下右键并拖拽或或使用三根手指滑动</li></ul> |




[雷达校准](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/lidar_calibration_cn.pdf)

[雷达IMU校准](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/apollo_lidar_imu_calibration_guide.md)


# ================================
# Apollo导航模式教程

## 1. 教程简介

无人驾驶系统利用实时感知信息和静态地图信息构建出完整驾驶环境，并在构建的环境中，依据routing数据，规划出行车轨迹，并由控制模块执行完成。Apollo导航模式在上述的框架下，针对高速、乡村道路等简单道路场景，进行了以下的提升：

1. Apollo导航模式以提高安全性和稳定性为目的，在驾驶环境中加入了静态引导信息，引导在驾驶环境中的轨迹规划，使其更安全更舒适。同时，引导信息也降低了对驾驶环境的完整性的要求 -- 即降低了对地图信息的要求。
2. Apollo导航模式使用了相对/车身坐标系。减少了sensor数据的转化。同时也支持各种驾驶模式之间的转化，以应对不同的驾驶场景和条件。
3. Apollo导航模式引入了百度地图的Routing功能，考虑实时路况信息，使得Routing的结果更实用，更精确，更稳定。也使得Apollo系统更易于落地和商用。



## 在本教程中，你将完成

学习完本教程后，你将能够在导航模式下进行规划模块（planning）的线下调试和开发。

## 在本教教中，你将掌握

- 如何设置Apollo导航模式
- 如何利用云端指引者发送指引线
- 如何利用录制的ros bag产生指引线并用线下指引者发送
- 如何进行规划模块的调试



## 在本教程中，你需要如下准备

- 下载并编译Apollo最新源码（[Howto](https://github.com/ApolloAuto/apollo/tree/master/docs/demo_guide)）

- 下载 [Apollo2.5 demo bag](https://github.com/ApolloAuto/apollo/releases/download/v2.5.0/demo_2.5.bag)


## 2. 配置导航模式

在导航模式下，有以下几个参数需要进行配置：

- 感知方案：目前支持摄像头方案（CAMERA）和基于Mobileye的方案（MOBILEYE）
- Apollo UTM Zone
- 规划模块的Planner：目前支持EM, LATTICE, 和NAVI三种
- 系统限速：单位为米/秒

## 在Docker下修改配置文件

配置文件位于：

```bash
/apollo/modules/tools/navigation/config/default.ini
```

默认配置为：

```bash
[PerceptionConf]
# three perception solutions: MOBILEYE, CAMERA, and VELODYNE64
perception = CAMERA

[LocalizationConf]
utm_zone = 10

[PlanningConf]
# three planners are available: EM, LATTICE, NAVI
planner_type = EM

# highest speed for planning algorithms, unit is meter per second
speed_limit = 5
```

该默认配置为Apollo 2.5 Demo bag录制时的配置，在此教程中，我们直接使用。

## 生效配置信息

为了使配置生效，在Docker内的Apollo根目录下，运行如下命令

```bash
in_dev_docker:/apollo$ cd /apollo/modules/tools/navigation/config/
in_dev_docker:/apollo/modules/tools/navigation/config$ python navi_config.py default.ini
```

## 3. 云端指引者的使用

## 回放demo bag

在进入Docker，启动Apollo之前，我们把[Apollo2.5 demo bag](https://github.com/ApolloAuto/apollo/releases/download/v2.5.0/demo_2.5.bag) 拷贝到Apollo代码根目录下的data目录中。

在Docker内编译成功后，我们用如下命令启动Dreamview：

```bash
in_dev_docker:/apollo$ ./scripts/bootstrap.sh start
```

并在本地浏览器中打开

```bash
http://localhost:8888
```

如下图所示，在模式框中选择“Navigation”。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_1_init.png) 

然后在Docker内的apollo根目录下运行如下命令进行bag播放

```bash
in_dev_docker:/apollo$cd data
in_dev_docker:/apollo/data$rosbag play demo_2.5.bag
```

播放开始后，可以看到Dreamview界面如下

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_2_play.png)

## 请求云端指引线

在地图中选择一个目的地（沿canada路），点击地图视图中的红色Route按钮，云端指引者会接收到这个请求，并返回指引线，该指引线会被显示在地图视图中。如下图所示。

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_3_cloud.png)

以上就是云端指引者的调用过程。

## 4.  离线指引者工具的使用 

目前云端指引者只覆盖了有限的区域。除了云端的服务之外，我们还提供了离线指引者工具来制作和发送线下指引线。在本教程中，我们以[Apollo2.5 demo bag](https://github.com/ApolloAuto/apollo/releases/download/v2.5.0/demo_2.5.bag)为例来生成指引线。

## 指引线的制作

生成指引线的步骤为

- 从bag中提取路径数据

```bash
in_dev_docker:/apollo$cd modules/tools/navigator
in_dev_docker:/apollo/modules/tools/navigator$python extractor.py /apollo/data/demo_2.5.bag
```

提取出来的路径数据在路径

```bash
in_dev_docker:/apollo/modules/tools/navigator$
```

中的

```bash
path_demo_2.5.bag.txt
```

- 平滑路径数据

```bash
in_dev_docker:/apollo/modules/tools/navigator$bash smooth.sh path_demo_2.5.bag.txt 200
```

平滑后的的数据在

```bash
in_dev_docker:/apollo/modules/tools/navigator$path_demo_2.5.bag.txt.smoothed
```

## 指引线的发送

得到平滑后的数据就可以发送到Apollo系统中，作为指引线，步骤为：

```bash
in_dev_docker:/apollo/modules/tools/navigator$python navigator.py path_demo_2.5.bag.txt.smoothed
```

发送完成后，Dreamview的地图视图中的红色指引线会更新为如下图所示：

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_4_offline.png)

## 5. 规划模块的调试

## 调试数据准备

利用bag来进行模块调试，首先要把bag中的相应ros message过滤掉。假设我们想要调试规划模块，我们需要把消息

```
/apollo/planning
```

过滤，使用以下命令

```bash
in_dev_docker:/apollo$cd data
in_dev_docker:/apollo/data$rosbag filter demo_2.5.bag demo_2.5_no_planning.bag "topic != '/apollo/planning'"
```

过滤后的bag位于

```bash
in_dev_docker:/apollo/data$demo_2.5_no_planning.bag
```

## 规划轨迹的产生

我们播放没有规划的bag，用下面的命令

```bash
in_dev_docker:/apollo/data$rosbag play demo_2.5_no_planning.bag
```

在Dreamview中我们会看到车辆的规划轨迹没有输出，如下图

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_5_no_planning.png)

我们在Dreamview中打开Navi Planning模块，如下图

![img](https://github.com/ApolloAuto/apollo/blob/master/docs/technical_tutorial/images/navigation_mode_tutorial/navigation_mode_6_live_planning.png)

我们看到实时计算的车辆的规划轨迹显示在Dreamview中。这时你可以试着更改一些规划模块的配置

```
in_dev_docker:/apollo/modules/planning/conf$planning_config_navi.pb.txt
```

去了解，这些参数会对规划结果有什么影响。或者修改规划算法的代码，进行调试。

## 6.结束

恭喜你完成了本教程。现在你应该了解

- 如何设置Apollo导航模式
- 如何利用云端指引者发送指引线
- 如何利用录制的ros bag产生指引线并用线下指引者发送
- 如何进行规划模块的调试

你也可以试着利用demo bag对其他一些模块进行调试。


# =========================
# 多激光雷达全球导航卫星系统(Multiple-LiDAR GNSS)校准指南

欢迎使用多激光雷达全球导航卫星系统校准工具。本指南将向您展示如何成功校准多个LiDAR的步骤。

## 内容

-	概述
-	准备
-	使用校准工具
-	结果与验证

## 概述

在许多自动驾驶任务，如HDMap的制作，多个激光雷达扫描结果需要注册在一个统一的坐标系统。在这种情况下，需要对多个LIDARs的外部参数进行仔细校准。为了解决这个问题，开发了多激光雷达GNSS校准工具。

## 准备

下载校准工具，并将文件提取到$APOLLO_HOME/modules /calibration。$APOLLO_HOME是APOLLO repository的根目录。
根据Apollo 1.5提供的校准指南选择校准位置。
确保GNSS处于良好状态。为了验证这一点，使用‘rostopic echo /apollo/sensor/gnss/best_pose’并检查关键词latitude_std_dev, longitude_std_dev 和height_std_dev后的数量，偏差越小，校准质量越好。 我们强烈建议在偏差小于0.02时校准传感器。
## 使用校准工具

### 记录校准数据

当LIDARS和GNSS准备就绪时，使用/apollo/modules/calibration/multi_lidar_gnss/record.sh记录校准数据。请注意，此脚本仅用于记录velodyne HDL64 和VLP16。为了其他目的，需要修改这个脚本，或者只需要使用rosbag record来做同样的事情。通常，2分钟的数据长度就足够了。在数据捕获之后，运行/apollo/modules/calibration/multi_lidar_gnss/calibrate.sh校准传感器。脚本由以下两个步骤组成。

### 出口数据

一旦校准包被记录，使用/apollo/modules/calibration/exporter/export_msgs --config /apollo/modules/calibration/exporter/conf/export_config.yaml获得传感器数据。exporter的唯一输入是一个YAML配置文件，如下所示。
```bash
bag_path: "/apollo/data/bag/calibration/" # The path where the calibration bag is placed.
dump_dir: "/apollo/data/bag/calibration/export/" # The path where the sensor data will be placed using exporter
topics:
    - /apollo/sensor/gnss/odometry: # Odometry topic name
        type: ApolloOdometry        # Odometry type
    - /apollo/sensor/velodyne16/PointCloud2: # vlp16 topic name
        type: PointCloud2                    # vlp16 type
    - /apollo/sensor/velodyne64/PointCloud2: # hdl64 topic name
        type: PointCloud2                    # hdl64 type
```

如果将新topic按如下的规则添加到文件中，也可以导出PointCloud2 types的其他topic。
```bash
    - TOPIC_NAME: # topic name
        type: PointCloud2
```

到目前为止，我们只支持ApolloOdometry和PointCloud2。

### 运行校准工具

如果输出所有传感器数据，运行/apollo/modules/calibration/lidar_gnss_calibrator/multi_lidar_gnss_calibrator --config /apollo/modules/calibration/lidar_gnss_calibrator/conf/multi_lidar_gnss_calibrator_config.yaml将得到结果。该工具的输入是一个YAML配置文件，如下所示。
```bash
# multi-LiDAR-GNSS calibration configurations
data:
    odometry: "/apollo/data/bag/calibration/export/multi_lidar_gnss/_apollo_sensor_gnss_odometry/odometry"
    lidars: 
        - velodyne16: 
            path: "/apollo/data/bag/calibration/export/multi_lidar_gnss/_apollo_sensor_velodyne16_PointCloud2/"
        - velodyne64: 
            path: "/apollo/data/bag/calibration/export/multi_lidar_gnss/_apollo_sensor_velodyne64_PointCloud2/"
    result: "/apollo/data/bag/calibration/export/multi_lidar_gnss/result/"
calibration:
    init_extrinsics:
        velodyne16:
            translation:    
                x: 0.0
                y: 1.77 
                z: 1.1
            rotation:
                x: 0.183014 
                y: -0.183014 
                z: 0.683008 
                w: 0.683008
        velodyne64:
            translation:    
                x: 0.0
                y: 1.57
                z: 1.3
            rotation:
                x: 0.0
                y: 0.0
                z: 0.707
                w: 0.707
    steps: 
        - source_lidars: ["velodyne64"]
          target_lidars: ["velodyne64"]
          lidar_type: "multiple"
          fix_target_lidars: false
          fix_z: true
          iteration: 3
        - source_lidars: ["velodyne16"]
          target_lidars: ["velodyne16"]
          lidar_type: "multiple"
          fix_target_lidars: false
          fix_z: true
          iteration: 3
        - source_lidars: ["velodyne16"]
          target_lidars: ["velodyne64"]
          lidar_type: "multiple"
          fix_target_lidars: true
          fix_z: false
          iteration: 3
```

数据部分告诉工具在哪里获取点云和测距文件，以及在哪里保存结果。注意，LIDAR节点中的关键字将被识别为LiDARs的Frame ID。

校准部分提供了外部信息的初始猜测。所有的外部信息都是从激光雷达到GNSS，这意味着这种变换将激光雷达坐标系中定义的点的坐标映射到GNSS坐标系中定义的这一点的坐标。初始猜测要求旋转角度误差小于5度，平移误差小于0.1米。

步骤部分详细说明了校准过程。每个步骤被如下定义并且它们的含义在注释中。
```bash
- source_lidars: ["velodyne16"] # Source LiDAR in point cloud registration.
  target_lidars: ["velodyne64"] # Target LiDAR in point cloud registration.
  lidar_type: "multiple" # "multiple" for multi-beam LiDAR, otherwise "single"
  fix_target_lidars: true # Whether to fix  extrinsics of target LiDARS. Only "true" when align different LiDARs.
  fix_z: false # Whether to fix the z component of translation. Only "false" when align different LiDARs.
  iteration: 3 # Iteration number
```
## 结果和验证
校准工具将结果保存到结果路径中。
```bash
.
└── calib_result
    ├── velodyne16_novatel_extrinsics.yaml
    ├── velodyne16_result.pcd
    ├── velodyne16_result_rgb.pcd
    ├── velodyne64_novatel_extrinsics.yaml
    ├── velodyne64_result.pcd
    └── velodyne64_result_rgb.pcd
```
这两个YAML文件是外部的。为了验证结果，使用pcl_viewer *_result.pcd检查注册质量。如果传感器校准好了，大量的细节可以从点云中识别出来。欲了解更多详情，请参阅校准指南Apollo 1.5。



# ======================
# Apollo 2.0 传感器标定方法使用指南

欢迎使用Apollo传感器标定服务。本文档提供在Apollo 2.0中新增的3项传感器标定程序的使用流程说明，分别为：相机到相机的标定，相机到多线激光雷达的标定，以及毫米波雷达到相机的标定。

## 文档概览

* 概述
* 准备工作
* 标定流程
* 标定结果获取
* 标定结果验证

## 概述

在Apollo 2.0中，我们新增了3项标定功能：相机到相机的标定，相机到多线激光雷达的标定，以及毫米波雷达到相机的标定。对于多线激光雷达到组合惯导的标定，请参考多线激光雷达-组合惯导标定说明。Velodyne HDL64用户还可以使用Apollo 1.5提供的标定服务平台。标定工具均以车载可执行程序的方式提供。用户仅需要启动相应的标定程序，即可实时完成标定工作并进行结果验证。标定结果以 `.yaml` 文件形式返回。

## 准备工作

1. 下载[标定工具](https://github.com/ApolloAuto/apollo/releases/download/v2.0.0/calibration.tar.gz)，并解压缩到`$APOLLO_HOME/modules/calibration`目录下。（APOLLO_HOME是apollo代码的根目录）

2. 相机内参文件

	内参包含相机的焦距、主点和畸变系数等信息，可以通过一些成熟的相机标定工具来获得，例如 [ROS Camera Calibration Tools](http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration) 和 [Camera Calibration Toolbox for Matlab](http://www.vision.caltech.edu/bouguetj/calib_doc/)。内参标定完成后，需将结果转换为 `.yaml` 格式的文件。下面是一个正确的内参文件样例：

	```bash
	header: 
	  seq: 0
	  stamp: 
	    secs: 0
	    nsecs: 0
	  frame_id: short_camera
	height: 1080
	width: 1920
	distortion_model: plumb_bob
	D: [-0.535253, 0.259291, 0.004276, -0.000503, 0.0]
	K: [1959.678185, 0.0, 1003.592207, 0.0, 1953.786100, 507.820634, 0.0, 0.0, 1.0]
	R: [1.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 1.0]
	P: [1665.387817, 0.0, 1018.703332, 0.0, 0.0, 1867.912842, 506.628623, 0.0, 0.0, 0.0, 1.0, 0.0]
	binning_x: 0
	binning_y: 0
	roi: 
	  x_offset: 0
	  y_offset: 0
	  height: 0
	  width: 0
	  do_rectify: False
	```

	我们建议每一只相机都需要单独进行内参标定，而不是使用统一的内参结果。这样可以提高外参标定的准确性。

3. 初始外参文件

	本工具需要用户提供初始的外参值作为参考。一个良好的初始值可以帮助算法得到更精确的结果。下面是一个正确的相机到激光雷达的初始外参文件样例，其中translation为相机相对激光雷达的平移距离关系，rotation为旋转矩阵的四元数表达形式：

	```bash
	header:
	  seq: 0
	  stamp:
	    secs: 0
	    nsecs: 0
	  frame_id: velodyne64
	child_frame_id: short_camera
	transform:
	  rotation:
	    y: 0.5
	    x: -0.5
	    w: 0.5
	    z: -0.5
	  translation:
	    x: 0.0
	    y: 1.5
	    z: 2.0
	```

	注意：相机到激光雷达的标定方法比较依赖于初始外参值的选取，一个偏差较大的外参，有可能导致标定失败。所以，请在条件允许的情况下，尽可能提供更加精准的初始外参值。

4. 标定场地

	我们的标定方法是基于自然场景的，所以一个理想的标定场地可以显著地提高标定结果的准确度。我们建议选取一个纹理丰富的场地，如有树木，电线杆，路灯，交通标志牌，静止的物体和清晰车道线。图1是一个较好的标定环境示例：

	![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/calibration_place.png)
	<p align="center"> 图1 一个良好的标定场地 </p>

5. 所需Topics
	
	确认程序所需传感器数据的topics均有输出。如何查看传感器有数据输出？

	各个程序所需的topics如下表1-表3所示：
	
	表1. 相机到相机标定所需topics

	| 传感器       | Topic名称                                 |Topic发送频率（Hz）|
	| ------------ | ----------------------------------------- | ----------------- |
	| Short_Camera | /apollo/sensor/camera/traffic/image_short | 9                 |
	| Long_Camera  | /apollo/sensor/camera/traffic/image_long  | 9                 |
	| INS          | /apollo/sensor/gnss/odometry              | 100               |
	| INS          | /apollo/sensor/gnss/ins_stat              | 2                 |

	表2. 相机到64线激光雷达标定所需topics

	| 传感器       | Topic名称                                 |Topic发送频率（Hz）|
	| ------------ | ----------------------------------------- | ----------------- |
	| Short_Camera | /apollo/sensor/camera/traffic/image_short | 9                 |
	| LiDAR  | /apollo/sensor/velodyne64/compensator/PointCloud2  | 10                |
	| INS          | /apollo/sensor/gnss/odometry              | 100               |
	| INS          | /apollo/sensor/gnss/ins_stat              | 2                 |
	
	表3. 毫米波雷达到相机标定所需topics

	| 传感器       | Topic名称                                 |Topic发送频率（Hz）|
	| ------------ | ----------------------------------------- | ----------------- |
	| Short_Camera | /apollo/sensor/camera/traffic/image_short | 9                 |
	| INS          | /apollo/sensor/gnss/odometry              | 100               |
	| INS          | /apollo/sensor/gnss/ins_stat              | 2                 |

## 标定流程

所有标定程序需要用到车辆的定位结果。请确认车辆定位状态为56，否则标定程序不会开始采集数据。输入以下命令可查询车辆定位状态：

	```bash
	rostopic echo /apollo/sensor/gnss/ins_stat
    ```

### 相机到相机

1. 运行方法

	使用以下命令来启动标定工具：
	
	```bash
	cd /apollo/scripts
	bash sensor_calibration.sh camera_camera
	```

2. 采集标定数据
	* 由于两个相机的成像时间无法完全同步，所以在录制数据的时候，尽量将车辆进行慢速行驶，可以有效地缓解因时间差异所引起的图像不匹配问题。
	* 两个相机需有尽量大的图像重叠区域，否则该工具将无法进行外参标定运算。

3. 配置参数

	配置文件保存在以下路径，详细说明请参照表4。
	
	```bash
	/apollo/modules/calibration/camera_camera_calibrator/conf/camera_camera_calibrtor.conf
	```

	表4. 相机到相机标定程序配置项说明
	
	|配置项             | 说明               |
	|----------------- | ----------------  |
	|long_image_topic  | 长焦相机的图像topic |
	|short_image_topic | 广角相机的图像topic |
	|odometry_topic    | 车辆定位topic      |
	|ins_stat_topic    | 车辆定位状态topic   |
	|long_camera_intrinsics_filename  | 长焦相机的内参文件路径  |
	|short_camera_intrinsics_filename | 广角相机的内参文件路径  |
	|init_extrinsics_filename | 初始外参文件路径  |
	|output_path	   | 标定结果输出路径    |
	|max_speed_kmh     | 最大车速限制，单位km/h  |

4. 输出内容

	* 外参文件： 长焦相机到广角相机的外参文件。
	* 验证参考图片：包括一张长焦相机图像、一张广角相机图像及一张长焦相机依据标定后的外参投影到广角相机的去畸变融合图像。

### 相机到多线激光雷达

1. 运行方法

	使用以下命令来启动标定工具：
	
	```bash
	cd /apollo/scripts
	bash sensor_calibration.sh lidar_camera
	```

2. 采集标定数据
	* 为避免时间戳不同步，在录制数据的时候，尽量将车辆进行慢速行驶，可以有效地缓解因时间差异所引起的标定问题。
	* 相机中需看到一定数量的投影点云，否则该工具将无法进行外参标定运算。因此，我们建议使用短焦距相机来进行相机-激光雷达的标定。

3. 配置参数

	配置文件保存在以下路径，详细说明请参照表5。
	
	```bash
	/apollo/modules/calibration/lidar_camera_calibrator/conf/lidar_camera_calibrtor.conf
	```

	表5. 相机到多线激光雷达标定程序配置项说明
	
	配置项 | 说明
	--- | ---
	image_topic | 相机的图像topic
	lidar_topic | LiDAR的点云topic
	odometry_topic | 车辆定位topic
	ins_stat_topic | 车辆定位状态topic
	camera_intrinsics_filename	| 相机的内参文件路径
	init_extrinsics_filename | 初始外参文件路径
	output_path	| 标定结果输出路径
	calib_stop_count | 标定所需截取的数据站数
	max_speed_kmh | 最大车速限制，单位km/h

4. 输出内容
	
	* 外参文件：相机到多线激光雷达的外参文件。
	* 验证参考图片：两张激光雷达点云利用标定结果外参投影到相机图像上的融合图像，分别是依据点云深度渲染的融合图像，和依据点云反射值渲染的融合图像。

### 毫米波雷达到相机

1. 运行方法

	使用以下命令来启动标定工具：
	
	```bash
	cd /apollo/scripts
	bash sensor_calibration.sh radar_camera
	```

2. 采集标定数据

	* 请将车辆进行低速直线行驶，标定程序仅会在该条件下开始采集数据。

3. 配置参数

	配置文件保存在以下路径，详细说明请参照表6。
	
	```bash
	/apollo/modules/calibration/radar_camera_calibrator/conf/radar_camera_calibrtor.conf
	```

	表6. 相机到毫米波雷达标定程序配置项说明
	
	配置项 | 说明
	--- | ---
	image_topic | 相机的图像topic
	radar_topic | Radar的数据topic
	odometry_topic | 车辆定位topic
	ins_stat_topic | 车辆定位状态topic
	camera_intrinsics_filename	| 相机的内参文件路径
	init_extrinsics_filename | 初始外参文件路径
	output_path	| 标定结果输出路径
	max_speed_kmh | 最大车速限制，单位km/h

4. 输出内容
	
	* 外参文件：毫米波雷达到短焦相机的外参文件。
	* 验证参考图片：将毫米波雷达投影到激光雷达坐标系的结果，需运行 `radar_lidar_visualizer` 工具。具体方法可参阅 `标定结果验证` 章节。

## 标定结果获取

所有标定结果均保存在配置文件中所设定的 `output` 路径下，标定后的外参以 `yaml` 格式的文件提供。此外，根据传感器的不同，标定结果会保存在 `output` 目录下的不同文件夹中，具体如表7所示：

表7. 标定结果保存路径

| 传感器        | 外参保存路径            |
| ------------ | -----------------------|
| Short_Camera | [output]/camera_params |
| Long_Camera  | [output]/camera_params |
| Radar        | [output]/radar_params  |

## 标定结果验证

当标定完成后，会在 `[output]/validation` 目录下生成相应的标定结果验证图片。下面会详细介绍每一类验证图片的基本原理和查看方法。

### 相机到相机标定

* 基本方法：根据长焦相机投影到短焦相机的融合图像进行判断，绿色通道为短焦相机图像，红色和蓝色通道是长焦投影后的图像，目视判断检验对齐情况。在融合图像中的融合区域，选择场景中距离较远处（50米以外）的景物进行对齐判断，能够重合则精度高，出现粉色或绿色重影（错位），则存在误差，当误差大于一定范围时（范围依据实际使用情况而定），标定失败，需重新标定（正常情况下，近处物体因受视差影响，在水平方向存在错位，且距离越近错位量越大，此为正常现象。垂直方向不受视差影响）。

* 结果示例：如下图所示，图2为满足精度要求外参效果，图3为不满足精度要求的现象，请重新进行标定过程。

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/cam_cam_good.png)
<p align="center"> 图2 良好的相机到相机标定结果 </p>

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/cam_cam_error.png)
<p align="center"> 图3 错误的相机到相机标定结果 </p>

### 相机到多线激光雷达标定

* 基本方法：在产生的点云投影图像内，可寻找其中具有明显边缘的物体和标志物，查看其边缘轮廓对齐情况。如果50米以内的目标，点云边缘和图像边缘能够重合，则可以证明标定结果的精度很高。反之，若出现错位现象，则说明标定结果存在误差。当误差大于一定范围时（范围依据实际使用情况而定），该外参不可用。

* 结果示例：如下图所示，图4为准确外参的点云投影效果，图5为有偏差外参的点云投影效果

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/cam_lidar_good.png)
<p align="center"> 图4 良好的相机到多线激光雷达标定结果 </p>

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/cam_lidar_error.png)
<p align="center"> 图5 错误的相机到多线激光雷达标定结果 </p>

### 毫米波雷达到相机
	
* 基本方法：为了更好地验证毫米波雷达与相机间外参的标定结果，引入激光雷达作为桥梁，通过同一系统中毫米波雷达与相机的外参和相机与激光雷达的外参，计算得到毫米波雷达与激光雷达的外参，将毫米波雷达数据投影到激光雷达坐标系中与激光点云进行融合，并画出相应的鸟瞰图进行辅助验证。在融合图像中，白色点为激光雷达点云，绿色实心圆为毫米波雷达目标，通过图中毫米波雷达目标是否与激光雷达检测目标是否重合匹配进行判断，如果大部分目标均能对应匹配，则满足精度要求，否则不满足，需重新标定。

* 结果示例：如下图所示，图6为满足精度要求外参效果，图7为不满足精度要求外参效果。

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/radar_cam_good.png)
<p align="center"> 图6 良好的毫米波雷达到激光雷达投影结果 </p>

![](https://github.com/ApolloAuto/apollo/tree/master/docs/quickstart/images/calibration/sensor_calibration/radar_cam_error.png)
<p align="center"> 图7 错误的毫米波雷达到激光雷达投影结果 </p>

* 注意事项：
	* 为了得到毫米波雷达目标和激光雷达点云融合的验证图像，系统会自动或手动调用毫米波雷达到激光雷达的投影工具（`radar_lidar_visualizer`）进行图像绘制和生成过程。该投影工具在启动时会自动载入毫米波雷达与相机的外参文件及相机与激光雷达的外参文件，因此在启动之前，需要先进行相应的标定工具或将两文件以特定的文件名放在相应路径中，以备工具调用。

	* 使用以下命令来启动 `radar_lidar_visualizer` 工具：
	
		```bash
		cd /apollo/scripts
		bash sensor_calibration.sh visualizer
		```

	* `radar_lidar_visualizer` 工具的配置文件在以下路径，详细说明请参照表8。
	
		```bash
		/apollo/modules/calibration/radar_lidar_visualizer/conf/radar_lidar_visualizer.conf
		```
	
		表8. 毫米波雷达到激光雷达投影工具配置项说明

		配置项 | 说明
		--- | ---
		radar_topic | Radar的数据topic
		lidar_topic | LiDAR的点云topic
		radar_camera_extrinsics_filename | 毫米波雷达到相机的外参文件
		camera_lidar_extrinsics_filename | 相机到激光雷达的外参文件
		output_path	| 标定结果输出路径

	* 验证图片同样保存在 `[output]/validation` 目录下。


