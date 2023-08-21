cmake_minimum_required(VERSION 3.13)

project(googletest_sample)

add_library(sumLibrary STATIC LibraryCode.cpp)

add_executable(mainApp main.cpp)
target_link_libraries(mainApp sumLibrary)

# 2nd step: get googletest (need git) and add test.cpp
include(FetchContent)
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest
    GIT_TAG v1.14.0)

FetchContent_GetProperties(googletest)
#googletest_POPULATE
#googletest_SOURCE_DIR
#googletest_BINARY_DIR
if(NOT googletest_POPULATE)
    FetchContent_Populate(googletest)
    add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})
endif()

add_executable(testRunner test.cpp)
target_link_libraries(testRunner sumLibrary gtest_main gmock_main)
