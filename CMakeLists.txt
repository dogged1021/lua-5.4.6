# CMakeLists.txt for building Lua

cmake_minimum_required ( VERSION 3.16 )
project ( lua )

# set ( CMAKE_GENERATOR "MinGW Makefiles" )
# set ( CMAKE_GENERATOR "Ninja" )
# message ( "generator is set to ${CMAKE_GENERATOR}" )

# 设置使用Ninja作为构建系统
set ( CMAKE_MAKE_PROGRAM "ninja" )

# set ( CMAKE_CXX_COMPILER "cl.exe" )
# set ( CMAKE_C_COMPILER "cl.exe" )
# set ( CMAKE_CXX_COMPILER "gcc" )
# set ( CMAKE_C_COMPILER "gcc" )

# release
set ( CMAKE_BUILD_TYPE Release )

set ( CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON )
set ( CMAKE_EXPORT_COMPILE_COMMANDS ON )
set ( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic -std=${CXX_STANDARD}" )
set ( CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g" )
set ( CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3" )
set ( CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl, --export-all-symbols" )

set ( INC ${CMAKE_CURRENT_SOURCE_DIR}/include )
set ( SRC ${CMAKE_CURRENT_SOURCE_DIR}/src )
set ( LUA ${CMAKE_CURRENT_SOURCE_DIR}/build/lua )

set ( CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR}/lua )
set ( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${LUA}/bin )
set ( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LUA}/bin )
set ( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${LUA}/bin )

set ( CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON )

link_directories ( ${LUA}/bin )
include_directories ( ${INC} )

add_subdirectory ( ${SRC} )
