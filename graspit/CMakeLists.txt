cmake_minimum_required(VERSION 2.8.3)
project(graspit)

set(PACKAGE_DEPS
)

find_package(catkin REQUIRED COMPONENTS ${PACKAGE_DEPS})
find_program(HAVE_QMAKE_QT_4 qmake-qt4)

if(HAVE_QMAKE_QT_4)
  set(QMAKE_COMMAND qmake-qt4)
else(NOT HAVE_QMAKE_QT_4)
  set(QMAKE_COMMAND qmake)
endif(HAVE_QMAKE_QT_4)
message("GraspIt built with ${QMAKE_COMMAND}")


catkin_package(
  CATKIN_DEPENDS ${PACKAGE_DEPS}
  INCLUDE_DIRS . graspit_source
)

include_directories(${catkin_INCLUDE_DIRS})
add_custom_command(
  OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND git submodule init
  COMMAND git submodule update
  COMMAND cd graspit && patch -N -d graspit_source -p0 < graspit_project.patch && cd ..
  COMMAND cd graspit && patch -N -d graspit_source -p0 < graspit_dbase.patch && cd ..
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/..
)
add_custom_target(graspit_build ALL
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND ${QMAKE_COMMAND}  "EXT_DESTDIR = ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_BIN_DESTINATION}" ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/graspit.pro
  COMMAND make
)

install(DIRECTORY graspit_source/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
