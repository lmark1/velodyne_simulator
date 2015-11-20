cmake_minimum_required(VERSION 2.8.3)
project(velodyne_gazebo_plugins)

find_package(catkin REQUIRED COMPONENTS
  tf
  gazebo_ros
  gazebo_plugins
  roscpp
  sensor_msgs
)
find_package(gazebo)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS tf gazebo_ros gazebo_plugins roscpp sensor_msgs
  DEPENDS gazebo
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
)

add_library(gazebo_ros_velodyne_laser src/VelodyneLaserPlugin.cpp)
target_link_libraries(gazebo_ros_velodyne_laser
  ${catkin_LIBRARIES}
  ${GAZEBO_LIBRARIES}
)

install(TARGETS gazebo_ros_velodyne_laser
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
