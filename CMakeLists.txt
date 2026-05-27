cmake_minimum_required(VERSION 3.10)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"
)

project(print)



set(PRINT_VERSION_MAJOR 0)
set(PRINT_VERSION_MINOR 1)
set(PRINT_VERSION_PATCH 0)
set(PRINT_VERSION_TWEAK 0)
set(PRINT_VERSION
  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
set(PRINT_VERSION_STRING "v${PRINT_VERSION}")

option(BUILD_EXAMPLES "Build examples" OFF)

option(BUILD_TESTS "Build tests" OFF)


add_library(print STATIC src/print.cpp)

target_include_directories(print PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)


if(BUILD_TESTS)
    hunter_add_package(GTest)
    find_package(GTest CONFIG REQUIRED)

    add_executable(check tests/test1.cpp)
    target_link_libraries(check PRIVATE print GTest::gtest_main)
    add_test(NAME check COMMAND check)
endif()


include(CPackConfig.cmake)
