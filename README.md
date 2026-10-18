# bsa-ros2-demo FROM ros:jazzy-ros-base

RUN apt-get update && \
    apt-get install -y python3-colcon-common-extensions && \
    rm -rf /var/lib/apt/lists/*
    {
  "name": "ROS 2 Jazzy Development",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "remoteUser": "root"
}
<?xml version="1.0"?>
<package format="3">
  <name>bsa_status_publisher</name>
  <version>0.0.1</version>
  <description>ROS 2 BSA status publisher demo</description>

  <maintainer email="developer@example.com">Developer</maintainer>
  <license>Apache-2.0</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <depend>rclcpp</depend>
  <depend>std_msgs</depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>

cmake_minimum_required(VERSION 3.8)
project(bsa_status_publisher)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(bsa_status_publisher_node
  src/main.cpp
)

ament_target_dependencies(
  bsa_status_publisher_node
  rclcpp
  std_msgs
)

install(
  TARGETS bsa_status_publisher_node
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()

src/bsa_status_publisher/src/main.cpp

source /opt/ros/jazzy/setup.bash

sudo apt-get update
sudo apt-get install -y python3-colcon-common-extensions

cd /workspaces/bsa-ros2-demo

rosdep update
rosdep install --from-paths src --ignore-src -r -y

colcon build --packages-select bsa_status_publisher

source install/setup.bash

ros2 run bsa_status_publisher bsa_status_publisher_node

[INFO] [bsa_status_publisher]: Published BSA status: RIGHT_BLIND_SPOT_WARNING

source /opt/ros/jazzy/setup.bash
cd /workspaces/bsa-ros2-demo
source install/setup.bash

ros2 topic echo /bsa/status