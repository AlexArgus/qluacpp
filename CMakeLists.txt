cmake_minimum_required(VERSION 3.4.0)
project(qluacpp)

if (NOT QLUACPP_LUA_LIBRARY)
  message( FATAL_ERROR "Please set QLUACPP_LUA_LIBRARY variable to your Lua library file. For example:\n cmake -DQLUACPP_LUA_LIBRARY=c:\\lua\\lua51.lib ...")
endif()
message ("Lua library: ${QLUACPP_LUA_LIBRARY}")

if (NOT QLUACPP_LUA_INCLUDE_DIR)
  message( FATAL_ERROR "Please set QLUACPP_LUA_INCLUDE_DIR variable to the path to your lua.h file. For example:\n cmake -DQLUACPP_LUA_INCLUDE_DIR=c:\\lua\\include ...")
endif()
message ("Lua include dir: ${QLUACPP_LUA_INCLUDE_DIR}")

include_directories(
  ${LUACPP}/include
  ${QLUACPP_LUA_INCLUDE_DIR}
  )
set(SRC "./src")

set(SOURCES
  ${SRC}/qlua/qlua.cpp
  )

if (CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -std=c++1z")
endif()

if (UNIX)
  if (CMAKE_CXX_COMPILER_ID MATCHES "GNU")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC ")
  endif()
endif()

add_library(qluacpp ${SOURCES})
target_link_libraries(qluacpp ${QLUACPP_LUA_LIBRARY})
