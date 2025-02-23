cmake_minimum_required(VERSION 3.2)

project(tinyxml VERSION 2.8.2 LANGUAGES CXX)

if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
endif()

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_library(tinyxml
  tinyxml.h
  tinyxml.cpp
  tinyxmlerror.cpp
  tinyxmlparser.cpp
)

target_compile_definitions(tinyxml
  PRIVATE
  TIXML_USE_STL
  _CRT_SECURE_NO_DEPRECATE
  _CRT_NONSTDC_NO_DEPRECATE
  INTERFACE
  TIXML_USE_STL
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/tinyxml-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)
install(TARGETS tinyxml EXPORT tinyxml
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib)
install(FILES
  tinystr.h
  tinyxml.h
  DESTINATION include)
