# [iG-LIO](https://github.com/zijiechenrobotics/ig_lio) converter to [HDMapping](https://github.com/MapsHD/HDMapping)

## Hint

Please change branch to [Bunker-DVI-Dataset-reg-1](https://github.com/MapsHD/benchmark-iG-LIO-to-HDMapping/tree/Bunker-DVI-Dataset-reg-1) for quick experiment.  


## Dependecies
```shell
sudo apt install nlohmann-json3-dev
```

## Intended use 

This small toolset allows to integrate SLAM solution provided by [ig_lio](https://github.com/zijiechenrobotics/ig_lio) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 1 workspace that :
  - submodule to tested revision of iG LIO
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.


## Modify
```shell
src/ig_lio/config/ncd.yaml

lidar_topic: /os1_cloud_node/points
imu_topic: /os1_cloud_node/imu

to:

lidar_topic: /os1_cloud_node1/points
imu_topic: /os1_cloud_node1/imu
```
## Building

```shell
mkdir -p /test_ws/src
cd /test_ws/src
git clone https://github.com/marcinmatecki/iG-LIO-to-HDMapping.git --recursive
cd ..
catkin_make
```

## Usage - data SLAM:

Prepare recorded bag with estimated odometry:

In first terminal record bag:
```shell
rosbag record /current_scan /lio_odom
```

and start odometry:
```shell 
cd /test_ws/
source ./devel/setup.sh # adjust to used shell
roslaunch ig_lio lio_ncd.launch 
rosbag play {path_to_bag}
```

## Usage - conversion:

```shell
cd /test_ws/ros_ws
source ./devel/setup.sh # adjust to used shell
rosrun ig-lio-to-hdmapping listener <recorded_bag> <output_dir>
```

## Record the bag file:

```shell
rosbag record /current_scan /lio_odom -o {your_directory_for_the_recorded_bag}
```

## ig LIO Launch:

```shell
cd /test_ws/
source ./devel/setup.sh # adjust to used shell
roslaunch ig_lio lio_ncd.launch
rosbag play {path_to_bag}
```

## During the record (if you want to stop recording earlier) / after finishing the bag:

```shell
In the terminal where the ros record is, interrupt the recording by CTRL+C
Do it also in ros launch terminal by CTRL+C.
```

## Usage - Conversion (ROS bag to HDMapping, after recording stops):

```shell
cd /test_ws/
source ./devel/setup.sh # adjust to used shell
rosrun ig-lio-to-hdmapping listener <recorded_bag> <output_dir>
```
