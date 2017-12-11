cmake_minimum_required(VERSION 2.8.3)
project(ros_control_robot)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS
    roscpp
    combined_robot_hw
    std_msgs
    controller_manager
    ros_ethercat_model
    realtime_tools
    diagnostic_updater
    diagnostic_msgs
    pluginlib
    cmake_modules
)

find_package(TinyXML REQUIRED)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${TinyXML_INCLUDE_DIRS}
)

catkin_package(
DEPENDS
CATKIN_DEPENDS
    roscpp
    combined_robot_hw
    std_msgs
    controller_manager
    ros_ethercat_model
    realtime_tools
    diagnostic_updater
    diagnostic_msgs
    pluginlib
)

add_executable(${PROJECT_NAME} src/main.cpp)
target_link_libraries(${PROJECT_NAME} rt ${catkin_LIBRARIES} ${TinyXML_LIBRARIES})
add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})
ros_enable_rpath(${PROJECT_NAME})

install(TARGETS ${PROJECT_NAME}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

