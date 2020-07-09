cmake_minimum_required(VERSION 3.0.2)
project(sainsmart_relay_usb)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
)

catkin_package()

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME}_node src/RelayNode.cpp src/node.cpp)
target_link_libraries(${PROJECT_NAME}_node ${catkin_LIBRARIES} ftdi)
set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME relay_node PREFIX "")

add_executable(${PROJECT_NAME}_list src/list.cpp)
target_link_libraries(${PROJECT_NAME}_list ${catkin_LIBRARIES} ftdi)
set_target_properties(${PROJECT_NAME}_list PROPERTIES OUTPUT_NAME list PREFIX "")

install(TARGETS ${PROJECT_NAME}_node ${PROJECT_NAME}_list
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

if(CATKIN_BUILD_BINARY_PACKAGE)
  # Install udev rules with dh_installudev: http://manpages.ubuntu.com/manpages/man1/dh_installudev.1.html
  FILE(REMOVE ${CMAKE_CURRENT_SOURCE_DIR}/debian/udev)
  FILE(GLOB UDEV_FILES RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}/udev" "${CMAKE_CURRENT_SOURCE_DIR}/udev/*.rules")
  FOREACH(FILENAME ${UDEV_FILES})
    MESSAGE(STATUS "Appending contents of udev/${FILENAME} to debian/udev")
    FILE(READ udev/${FILENAME} FILEDATA)
    FILE(APPEND ${CMAKE_CURRENT_SOURCE_DIR}/debian/udev ${FILEDATA})
  ENDFOREACH(FILENAME)
else()
  install(DIRECTORY udev
          DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  )
endif()

