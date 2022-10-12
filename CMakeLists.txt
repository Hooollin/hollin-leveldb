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

include_directories(
  "${PROJECT_BINARY_DIR}/include"
  "."
)

add_library(leveldb "") 
target_sources(leveldb
  PRIVATE
  "util/cache.cc"
  "util/coding.cc"
  "util/coding.h"
  "util/hash.cc"
  "util/hash.h"

  PUBLIC
  "${PROJECT_SOURCE_DIR}/include/leveldb/cache.h"
  "${PROJECT_SOURCE_DIR}/include/leveldb/slice.h"
)

target_include_directories(leveldb
  PUBLIC
  ${PROJECT_SOURCE_DIR}/include
)

add_executable(cache_test 
 "${PROJECT_SOURCE_DIR}/util/cache.cc"
)

target_link_libraries(cache_test leveldb)