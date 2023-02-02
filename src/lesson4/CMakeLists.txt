cmake_minimum_required(VERSION 3.0.2)
project(lesson4)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  laser_geometry
  nav_msgs
  roscpp
  sensor_msgs
  tf
  tf_conversions
)

find_package(catkin REQUIRED COMPONENTS ${ROS_CXX_DEPENDENCIES})

find_package(Boost REQUIRED COMPONENTS thread signals)

find_package(Eigen3)

if(NOT EIGEN3_FOUND)
  # Fallback to cmake_modules
  find_package(cmake_modules REQUIRED)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN_INCLUDE_DIRS})
  set(EIGEN3_LIBRARIES ${EIGEN_LIBRARIES})  # Not strictly necessary as Eigen is head only
  # Possibly map additional variables to the EIGEN3_ prefix.
else()
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
endif()

catkin_package(
 INCLUDE_DIRS include
#  LIBRARIES lesson4
 CATKIN_DEPENDS ${ROS_CXX_DEPENDENCIES}
#  DEPENDS system_lib
)


include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)


## occupancy_grid
add_executable(${PROJECT_NAME}_occupancy_grid_node
  src/occupancy_grid/occupancy_grid.cc
)
add_dependencies(${PROJECT_NAME}_occupancy_grid_node 
${catkin_EXPORTED_TARGETS}
)
target_link_libraries(${PROJECT_NAME}_occupancy_grid_node
  ${catkin_LIBRARIES}
)