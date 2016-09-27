cmake_minimum_required(VERSION 2.8.3)
project(graspit)

set(PACKAGE_DEPS
)

find_package(catkin REQUIRED COMPONENTS ${PACKAGE_DEPS})


catkin_package(
  CATKIN_DEPENDS ${PACKAGE_DEPS}
  INCLUDE_DIRS . graspit_source graspit_source/include/
)

set_directory_properties(PROPERTY ADDITIONAL_MAKE_CLEAN_FILES ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/)
file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source)
file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/graspit_source/include)

include_directories(${catkin_INCLUDE_DIRS})

add_subdirectory(graspit_source)

install(DIRECTORY graspit_source/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
