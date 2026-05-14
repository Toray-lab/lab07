
cmake_minimum_required(VERSION 3.10)

project(print)


option(BUILD_EXAMPLES "Build examples" OFF)

option(BUILD_TESTS "Build tests" OFF)


add_library(print STATIC src/print.cpp)

target_include_directories(print PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)


if(BUILD_TESTS)

  enable_testing()

  add_subdirectory(third-party/gtest)

  file(GLOB TEST_SOURCES tests/*.cpp)

  add_executable(check ${TEST_SOURCES})

  target_link_libraries(check print gtest_main)

  target_include_directories(check PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

  add_test(NAME check COMMAND check)

endif()

