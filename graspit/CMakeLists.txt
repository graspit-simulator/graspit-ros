cmake_minimum_required(VERSION 2.8.3)
project(graspit)

set(PACKAGE_DEPS
)

find_package(catkin REQUIRED COMPONENTS ${PACKAGE_DEPS})

catkin_package(
  CATKIN_DEPENDS ${PACKAGE_DEPS}
  INCLUDE_DIRS . graspit_source
)

include_directories(${catkin_INCLUDE_DIRS})

add_custom_target(graspit_build ALL
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND qmake "EXT_DESTDIR = ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_BIN_DESTINATION}" ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND make
)

install(DIRECTORY graspit_source/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)