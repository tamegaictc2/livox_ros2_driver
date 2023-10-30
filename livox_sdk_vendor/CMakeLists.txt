cmake_minimum_required(VERSION 3.9)

project(livox_sdk_vendor)

find_package(ament_cmake REQUIRED)

option(BUILTIN_livox_sdk "Force built-in version of livox-sdk" OFF)

list(INSERT CMAKE_MODULE_PATH 0 "${CMAKE_CURRENT_LIST_DIR}/cmake/Modules")

find_package(livox_sdk QUIET)

if(NOT livox_sdk_FOUND OR BUILTIN_livox_sdk)
  add_subdirectory(livox-sdk)
  set_property(TARGET livox_sdk_static PROPERTY POSITION_INDEPENDENT_CODE ON)
endif()

install(DIRECTORY cmake DESTINATION share/${PROJECT_NAME})

ament_package(CONFIG_EXTRAS livox_sdk_vendor-extras.cmake)
