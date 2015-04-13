cmake_minimum_required(VERSION 2.8)
project(osg-dae)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}")

include(FindPkgConfig)
pkg_check_modules(COLLADA REQUIRED collada-dom-141)
pkg_check_modules(OSG REQUIRED openscenegraph-osg)
include(OsgMacroUtils)

if (NOT COLLADA_FOUND)
    message(FATAL_ERROR "could not find the COLLADA library")
endif()
add_subdirectory(src)
