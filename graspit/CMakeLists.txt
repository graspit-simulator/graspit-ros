cmake_minimum_required(VERSION 2.8.3)
project(graspit)

set(PACKAGE_DEPS
  household_objects_database
)

find_package(catkin REQUIRED COMPONENTS ${PACKAGE_DEPS})

catkin_package(
  CATKIN_DEPENDS ${PACKAGE_DEPS}
  INCLUDE_DIRS . graspit_source
)

include_directories(${catkin_INCLUDE_DIRS})

add_custom_command(
  OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND svn co svn://svn.code.sf.net/p/graspit/code/trunk -r157 graspit_source
  COMMAND patch -N -d graspit_source -p0 < graspit_project.patch
  COMMAND patch -N -d graspit_source -p0 < graspit_dbase.patch
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_target(graspit_build ALL
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND qmake "EXT_DESTDIR = ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_BIN_DESTINATION}" ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND make
)

add_dependencies(graspit_build household_objects_database)

install(DIRECTORY graspit_source/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  PATTERN ".svn" EXCLUDE
)