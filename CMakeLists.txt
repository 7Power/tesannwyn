cmake_minimum_required(VERSION 2.6)

project(tesannwyn C)

set(CMAKE_MODULE_PATH "${tesannwyn_SOURCE_DIR}/cmake" "${CMAKE_MODULE_PATH}")

include(CMakeDependentOption)
include(CheckCCompilerFlag)
include(CheckCSourceCompiles)
check_c_compiler_flag("-Wall" HAVE_WALL_SWITCH)
if(HAVE_WALL_SWITCH)
    add_definitions("-Wall")
endif()

find_library(M_LIBRARY m REQUIRED)
set(CMAKE_REQUIRED_INCLUDES math.h)
set(CMAKE_REQUIRED_LIBRARIES m)

include_directories("${tesannwyn_SOURCE_DIR}")

set(SRCS tesannwyn.c)

set(HDRS defs.h funcs.h)

set(DATA_PATH "${tesannwyn_SOURCE_DIR}")
add_executable(tesannwyn ${SRCS} ${HDRS})
target_link_libraries(tesannwyn ${M_LIBRARY})
install(TARGETS tesannwyn RUNTIME DESTINATION bin)
