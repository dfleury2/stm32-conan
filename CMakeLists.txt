cmake_minimum_required(VERSION 3.21)

include(${CMAKE_CURRENT_BINARY_DIR}/conan_toolchain.cmake)

project(Stm32Baremetal)

find_package(bzip2 CONFIG REQUIRED)

add_library(example example.cpp)
target_link_libraries(example PUBLIC bzip2::bzip2)
