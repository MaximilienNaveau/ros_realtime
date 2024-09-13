cmake_minimum_required(VERSION 3.22.1)
project(lockfree)

#
# Options
#
option(BUILD_SHARED_LIBS "Build using shared libraries" ON)

#
# Handle dependencies by reading the package.xml
#
find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

ament_auto_add_library(${PROJECT_NAME} src/free_list.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

# ament_auto_add_gtest(test_freelist test/test_freelist.cpp)
# target_link_libraries(test_freelist ${PROJECT_NAME})

# ament_auto_add_gtest(test_object_pool test/test_object_pool.cpp)
# target_link_libraries(test_object_pool ${PROJECT_NAME})

#
# Handle install and exports.
#
install(DIRECTORY test/ DESTINATION share/${PROJECT_NAME})
ament_auto_package()