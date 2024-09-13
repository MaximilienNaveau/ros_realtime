cmake_minimum_required(VERSION 3.22.1)
project(rosatomic)

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

ament_auto_add_gtest(utest test/utest.cpp)

#
# Handle install and exports.
#
install(DIRECTORY test/ DESTINATION share/${PROJECT_NAME})
ament_auto_package()
