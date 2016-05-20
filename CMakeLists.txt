# Authors: Monica Reggiani, Claudio Pizzolato
cmake_minimum_required (VERSION 2.8.11) # "target_include_directories" command  and VS12 generator are missing in previous versions
project(RTOSIM CXX)
set(RTOSIM_MAJOR_VERSION 1)
set(RTOSIM_MINOR_VERSION 0)
set(RTOSIM_PATCH_VERSION 0)

#include GNUInstallDirs to get canonical paths
include(GNUInstallDirs)

if(WIN32)
    set(CMAKE_CXX_FLAGS "/EHsc")
endif()
if(UNIX AND NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel." FORCE)
endif()

if(UNIX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread -std=c++1y -Wno-deprecated-declarations")
endif(UNIX)

set(CMAKE_VERBOSE_MAKEFILE OFF)
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
find_package(OpenSim REQUIRED)

# Choose common build locations for executables and libraries
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_DEBUG_POSTFIX "d")

add_definitions(/D_USE_MATH_DEFINES)
add_subdirectory(lib)
add_subdirectory(src)
add_subdirectory(tests)