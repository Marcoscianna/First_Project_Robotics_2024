cmake_minimum_required(VERSION 2.8.3)
project(first_project)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
   roscpp nav_msgs tf
   sensor_msgs
   dynamic_reconfigure)

generate_dynamic_reconfigure_options(
    cfg/parameters.cfg
  )

catkin_package(
  CATKIN_DEPENDS roscpp std_msgs sensor_msgs)

include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(gps_to_odom src/gps_to_odom.cpp)
target_link_libraries(gps_to_odom ${catkin_LIBRARIES})

add_executable(odom_to_tf src/odom_to_tf.cpp)
target_link_libraries(odom_to_tf ${catkin_LIBRARIES})

add_executable(lidar_remap src/lidar_remap.cpp)
add_dependencies(lidar_remap ${PROJECT_NAME}_gencfg)
target_link_libraries(lidar_remap ${catkin_LIBRARIES})


