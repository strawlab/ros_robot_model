cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
set(ROS_BUILD_TYPE RelWithDebInfo)
rosbuild_init()
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

link_libraries(tinyxml)

rosbuild_add_library(collada_urdf src/collada_urdf.cpp)
rosbuild_link_boost(collada_urdf system)

rosbuild_add_executable(urdf_to_collada src/urdf_to_collada.cpp)
target_link_libraries(urdf_to_collada collada_urdf)

rosbuild_add_gtest(test_collada_writer test/test_collada_urdf.cpp)
target_link_libraries(test_collada_writer collada_urdf)
