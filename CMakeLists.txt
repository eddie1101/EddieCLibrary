cmake_minimum_required(VERSION 3.26)

set(PROJECT_VERSION 0.1.0)

project(ecl VERSION ${PROJECT_VERSION})

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_library(ecl SHARED
  src/ecl_ranges.c
)

target_sources(
  ecl
  PUBLIC
    FILE_SET public_headers
    TYPE HEADERS
    BASE_DIRS include
    FILES
      include/ecl.h
      include/ecl_ranges.h
)

target_include_directories(ecl PRIVATE include)
set_target_properties(ecl PROPERTIES
  VERSION ${PROJECT_VERSION}
  SOVERSION ${PROJECT_VERSION}
  ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib
  LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib
  RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)

include(GNUInstallDirs)

install(TARGETS ecl FILE_SET public_headers)


