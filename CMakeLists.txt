cmake_minimum_required(VERSION 3.0.2) 	
project(second_assignment)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  roscpp
  rospy
  stage_ros
  nav_msgs
  std_msgs
  std_srvs
  message_generation
)

add_message_files(
  FILES
  speedup.msg
 )
  
add_service_files(
   FILES
   speed.srv
 )
 
generate_messages(
   DEPENDENCIES
   geometry_msgs
   std_msgs
 )

catkin_package(
  INCLUDE_DIRS #include
  LIBRARIES second_assignment
  CATKIN_DEPENDS roscpp rospy stage_ros
  DEPENDS system_lib
)

include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

add_executable(drive_node src/control.cpp)
add_executable(speed_node src/interaction.cpp)

add_dependencies(drive_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
add_dependencies(speed_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

 target_link_libraries(drive_node
   ${catkin_LIBRARIES}
 )
 target_link_libraries(speed_node
   ${catkin_LIBRARIES}
 )
