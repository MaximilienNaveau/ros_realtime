cmake_minimum_required(VERSION 3.22.1)
project(allocators)

#
# Options
#
option(BUILD_SHARED_LIBS "Build using shared libraries" ON)

#
# Handle dependencies by reading the package.xml
#
find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

add_library(${PROJECT_NAME} INTERFACE)
target_include_directories(${PROJECT_NAME} PUBLIC INTERFACE
  $<INSTALL_INTERFACE:include>
)

ament_auto_add_gtest(test_aligned_alloc test/test_aligned_alloc.cpp)## Generate added messages and services with any dependencies listed here
#add_dependencies(test_aligned_alloc allocators_gencpp)

#
# Handle install and exports.
#
install(DIRECTORY test/ DESTINATION share/${PROJECT_NAME})
ament_auto_package()
