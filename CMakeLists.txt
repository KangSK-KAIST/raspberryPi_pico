cmake_minimum_required(VERSION 3.12)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(include/pico-sdk/pico_sdk_init.cmake)

project(my_project)

# initialize the Pico SDK
pico_sdk_init()

## Start of my project

# DEFINEs

# For __FILENAME__ to generate relative path only
string(LENGTH "${CMAKE_SOURCE_DIR}/" SOURCE_PATH_SIZE)
add_definitions("-DSOURCE_PATH_SIZE=${SOURCE_PATH_SIZE}")


# Build Type - Release and Debug
if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Select CMake build type." FORCE)
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release")
endif ()
string (TOUPPER "${CMAKE_BUILD_TYPE}" uppercase_CMAKE_BUILD_TYPE)
if (CMAKE_BUILD_TYPE AND NOT uppercase_CMAKE_BUILD_TYPE MATCHES "^(DEBUG|RELEASE)$")
  message (FATAL_ERROR "Invalid value for CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
endif ()


# Validation - Build Path
if (CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_CURRENT_BINARY_DIR AND NOT MSVC)
  message(FATAL_ERROR "In-source builds are not allowed.
  Please create a directory and build it there.")
endif ()


# Paths (to CMakeLists.txt)
set(PATH_MAIN ${PROJECT_SOURCE_DIR}/src)


# Source
set(SRC_MAIN
  ${PATH_MAIN}/main.c
)

# Libraries

# Validation - Library - pthread
# find_package(Threads REQUIRED)

set(INCLUDE_MAIN ${PROJECT_SOURCE_DIR}/src)

# Add executable
add_executable(
  main
  ${SRC_MAIN}
)

# Set include directories (local -I option for make)
target_include_directories(
  main
  PUBLIC
  ${INCLUDE_MAIN}
)
# Add pico_stdlib library which aggregates commonly used features
target_link_libraries(main pico_stdlib)
# create map/bin/hex/uf2 file in addition to ELF.
pico_add_extra_outputs(main)
