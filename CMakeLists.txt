cmake_minimum_required(VERSION 3.0.2)
project(viam_rover)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  rospy
  std_msgs
)

## Declare a catkin package
catkin_package()

## Specify additional locations of header files
include_directories(
  ${catkin_INCLUDE_DIRS}
)

## Install Python scripts
catkin_install_python(PROGRAMS
  scripts/example.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
