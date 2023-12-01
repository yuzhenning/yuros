# yuros: personal ROS-1 tb3 experiment system 
Build up a personal ROS-1 based Turtlebot3 Robot tracking control experiment system. <br/>
余的个人ROS-TURTLEBOT3 实验环境搭建方案

## Install Ubuntu 20.04
please make a u-disk system.<br/> 
ubuntu official web:<br/> 
<https://ubuntu.com/download> <br/> 
udisk software:<br/> 
1.rufus <br/> 
2.UltralISO

## Install ROS Noetic for Ubuntu 20.04
### STEP1: change ubuntu OS source to Tsinghua source
TsingHua website：<br/> 
<https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/>

replace codes as following:
```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

direction: /etc/apt/sources.list

### STEP 3: UPDATE
```
$ sudo apt-get update
```
### STEP 4: ROS INSTALL

在ubuntu20.04下安装Noetic版本ROS: <br/> 
添加ros源, 使用清华源: <br/> 
```
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```
增加key:
```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
安装ros:
```
sudo apt install ros-noetic-desktop-full
```

把ros环境加载脚本添加到bashrc 
```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

安装rosdep
```
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

添加清华源:
```
echo "export ROSDISTRO_INDEX_URL=https://mirrors.tuna.tsinghua.edu.cn/rosdistro/index-v4.yaml" >> ~/.bashrc
```

更新 rosdep
```
sudo rosdep init
rosdep update
```

或来自中国的源:
```
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
```

### STEP 5:  rosdep 工具包安装
根据很多2020年之前的资料，安装ROS后第一件事情是rosdep init， 但是2020年之后，这个指令不再有效。 <br/> 
我们根据最新情况，调整安装方案。
输入指令：升级rosdep
```
rosdep update
```
显示如下信息：
```
there is no rosdep command
rosdep init error:
```

fix: rosdep失效的解决方法
```
sudo apt install python3-rosdep2
```
重新安装部分ROS reinstall some part of ROS:
```
sudo apt --fix-broken install
sudo apt install ros-noetic-desktop-full
```

### STEP 6:  ROS Turtlebot3 机器人的工具包
由于turtlebot2 主要在indigo 系统,现已不再更新。本项目先择turtlebot3：

#### 6-1 python3 安装包
```
sudo apt install python3-rosinstall
sudo apt install python3-rosinstall-generator
sudo apt install python3-wstool
sudo apt install build-essential
```

#### 6-2 Turtlebot3 相关依赖包 注意版本：noetic
```
sudo apt-get install 
ros-noetic-joy 
ros-noetic-teleop-twist-joy 
ros-noetic-teleop-twist-keyboard 
ros-noetic-laser-proc 
ros-noetic-rgbd-launch 
ros-noetic-depthimage-to-laserscan 
ros-noetic-rosserial-arduino 
ros-noetic-rosserial-python 
ros-noetic-rosserial-server 
ros-noetic-rosserial-client 
ros-noetic-rosserial-msgs 
ros-noetic-amcl 
ros-noetic-map-server 
ros-noetic-move-base 
ros-noetic-urdf 
ros-noetic-xacro 
ros-noetic-compressed-image-transport 
ros-noetic-rqt-image-view 
ros-noetic-gmapping 
ros-noetic-navigation 
ros-noetic-interactive-markers
```

#### 6-3 git-clone ROBOTIS  TURTLEBOT3安装包
在工作空间：catkin_ws/src 地址下，输入以下安装包clone命令
```
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3.git
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3_simlulations.git
```

小Tips
github网速不好，经常掉线。需要多尝试几次。
其实这个方法是非常的简单，无需安装任何工具，毕竟也不合法，只需要在网址上添加fast关键词就可以！
比如要访问 http://githubfast.com，那么只需要在github后面加上fast就可以，也就是githubfast.com，那么就能正常访问。
```
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3.git
git clone https://githubfast.com/ROBOTIS-GIT/turtlebot3_simlulations.git
```

#### 6-4 生效工作空间
git-clone pkg之后注意，需要更新工作空间，用以下命令：
```
cd ~/catkin_ws/
catkin_make
```
之后会出一批结果，直到100%


<br/> 

<br/> 



