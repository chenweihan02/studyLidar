cmake_minimum_required(VERSION 3.0.2)
project(lesson2)


find_package(catkin REQUIRED COMPONENTS
  pcl_conversions
  pcl_ros
  roscpp
  sensor_msgs
)

find_package(PCL REQUIRED QUIET)

## catkin specific configuration ##
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES lesson2
#  CATKIN_DEPENDS pcl_conversions pcl_ros roscpp sensor_msgs
#  DEPENDS system_lib
)


## Build ##
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME}_scan_to_pointcloud2_converter_node
  src/scan_to_pointcloud2_converter.cc)

add_dependencies(${PROJECT_NAME}_scan_to_pointcloud2_converter_node
  ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

target_link_libraries(${PROJECT_NAME}_scan_to_pointcloud2_converter_node
  ${catkin_LIBRARIES})