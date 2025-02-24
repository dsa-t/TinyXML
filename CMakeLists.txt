cmake_minimum_required(VERSION 3.2)

project(tinyxml VERSION 2.8.2 LANGUAGES CXX)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_library(tinyxml
  tinyxml.h
  tinyxml.cpp
  tinyxmlerror.cpp
  tinyxmlparser.cpp
)

target_include_directories(tinyxml PUBLIC "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>")

target_compile_definitions(tinyxml
  PRIVATE
  TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
  INTERFACE
  TIXML_USE_STL
)

##
## Installation
##

## Standard modules
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

set(tinyxml_INSTALL_CMAKEDIR "${CMAKE_INSTALL_LIBDIR}/cmake/tinyxml")

## CMake targets and export scripts

install(
    TARGETS tinyxml EXPORT tinyxml-targets
    RUNTIME COMPONENT tinyxml_runtime
    LIBRARY COMPONENT tinyxml_runtime
    NAMELINK_COMPONENT tinyxml_development
    ARCHIVE COMPONENT tinyxml_development
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(
    EXPORT tinyxml-targets
    DESTINATION "${tinyxml_INSTALL_CMAKEDIR}"
    NAMESPACE tinyxml::
    FILE tinyxml-targets.cmake
    COMPONENT tinyxml_development
)

# Auto-generated version compatibility file
write_basic_package_version_file(
    tinyxml-config-version.cmake
    COMPATIBILITY SameMajorVersion
)

install(
    FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/tinyxml-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/tinyxml-config-version.cmake"
    DESTINATION "${tinyxml_INSTALL_CMAKEDIR}"
    COMPONENT tinyxml_development
)

## Headers

install(
    FILES tinystr.h tinyxml.h
    TYPE INCLUDE
    COMPONENT tinyxml2_development
)
