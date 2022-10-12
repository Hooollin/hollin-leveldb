cmake_minimum_required(VERSION 3.9)

project(leveldb VERSION 1.23.0 LANGUAGES C CXX)

# C standard can be overridden when this is used as a sub-project.
if(NOT CMAKE_C_STANDARD)
  # This project can use C11, but will gracefully decay down to C89.
  set(CMAKE_C_STANDARD 11)
  set(CMAKE_C_STANDARD_REQUIRED OFF)
  set(CMAKE_C_EXTENSIONS OFF)
endif(NOT CMAKE_C_STANDARD)

# C++ standard can be overridden when this is used as a sub-project.
if(NOT CMAKE_CXX_STANDARD)
  # This project requires C++11.
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  set(CMAKE_CXX_EXTENSIONS OFF)
endif(NOT CMAKE_CXX_STANDARD)

add_subdirectory("third_party/googletest")

include_directories(
  "${PROJECT_BINARY_DIR}/include"
  "."
)

add_library(leveldb "") 
target_sources(leveldb
  PRIVATE
  "util/arena.cc"
  "util/arena.h"
  "util/cache.cc"
  "util/coding.cc"
  "util/coding.h"
  "util/hash.cc"
  "util/hash.h"
  "util/random.h"

  PUBLIC
  "${PROJECT_SOURCE_DIR}/include/leveldb/cache.h"
  "${PROJECT_SOURCE_DIR}/include/leveldb/slice.h"
)

target_include_directories(leveldb
  PUBLIC
  ${PROJECT_SOURCE_DIR}/include
)

add_executable(cache_test 
 "${PROJECT_SOURCE_DIR}/util/cache_test.cc"
)

target_link_libraries(cache_test leveldb gmock gtest gtest_main)

add_executable(arena_test
 "${PROJECT_SOURCE_DIR}/util/arena_test.cc"
)

target_link_libraries(arena_test leveldb gmock gtest gtest_main)




