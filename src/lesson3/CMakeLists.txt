cmake_minimum_required(VERSION 3.0.2)
project(lesson3)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages

# List C++ dependencies on ros packages
set( ROS_CXX_DEPENDENCIES
  roscpp
  sensor_msgs
  geometry_msgs
  tf2
  tf2_geometry_msgs
  tf2_ros
)

find_package(catkin REQUIRED COMPONENTS ${ROS_CXX_DEPENDENCIES} )

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)

# Find csm project
find_package(PkgConfig)
pkg_check_modules(csm REQUIRED csm)


###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
 INCLUDE_DIRS include
 LIBRARIES lesson3
 CATKIN_DEPENDS ${ROS_CXX_DEPENDENCIES}
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${csm_INCLUDE_DIRS} 
)
link_directories(${csm_LIBRARY_DIRS})


# lesson3_scan_match_plicp_node
add_executable(${PROJECT_NAME}_scan_match_plicp_node src/scan_match_plicp.cc)

target_link_libraries( ${PROJECT_NAME}_scan_match_plicp_node 
  ${catkin_LIBRARIES} 
  ${csm_LIBRARIES}
)

add_dependencies(${PROJECT_NAME}_scan_match_plicp_node 
  ${csm_EXPORTED_TARGETS} 
  ${catkin_EXPORTED_TARGETS}
)

# lesson3_plicp_odometry_node
add_executable(${PROJECT_NAME}_plicp_odometry_node src/plicp_odometry.cc)

target_link_libraries( ${PROJECT_NAME}_plicp_odometry_node 
  ${catkin_LIBRARIES} 
  ${csm_LIBRARIES}
)

add_dependencies(${PROJECT_NAME}_plicp_odometry_node 
  ${csm_EXPORTED_TARGETS} 
  ${catkin_EXPORTED_TARGETS}
)
