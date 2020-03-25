cmake_minimum_required(VERSION 2.8.3)
project(yumi_hw)

set(CMAKE_BUILD_TYPE RelWithDebInfo)
add_definitions(-DROS=1)           # build using ROS libraries
add_definitions(-DLINUXSOCKETS=1)  # build using LINUX SOCKETS libraries

find_package(Boost REQUIRED COMPONENTS system thread QUIET)
find_package(abb_egm_interface QUIET)
find_package(abb_rws_interface QUIET)
LIST(APPEND CATKIN_DEPENDS_LIST
  cmake_modules
  control_toolbox
  controller_interface
  controller_manager
  hardware_interface
  joint_limits_interface
  kdl_parser
  realtime_tools
  roscpp
  std_msgs
  tf
  transmission_interface
  urdf
  message_generation
)


find_package(catkin REQUIRED COMPONENTS ${CATKIN_DEPENDS_LIST})

add_service_files(
  FILES
  YumiGrasp.srv
)

generate_messages(
  DEPENDENCIES
  std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS ${CATKIN_DEPENDS_LIST}
)
