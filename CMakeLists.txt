
#CMake file for dstart
#Author:weiyuanzu
#Create:20210702
#SET(CMAKE_C_COMPILER "/usr/local/bin/gcc")
#SET(CMAKE_CXX_COMPILER "/usr/local/bin/g++")
include(CheckCXXCompilerFlag)

cmake_minimum_required(VERSION 3.16)
#cmake_policy(SET CMP0015 OLD)
#定义工程名称
PROJECT(dstart_demo) 

MESSAGE(STATUS "Project Directory: ${PROJECT_SOURCE_DIR}")
set(CMAKE_CXX_STANDARD 11)
SET(CMAKE_BUILE_TYPE DEBUG) 

add_definitions(-DLinux)


#源文件
#FILE(GLOB_RECURSE SOURCE_FILES ${PROJECT_BINARY_DIR}/python_server/src/*.cpp) 
FILE(GLOB_RECURSE SOURCE_FILES ${PROJECT_SOURCE_DIR}/main.cpp)   


#相关头文件的目录    
INCLUDE_DIRECTORIES( 
  /usr/include/c++/6.1.0
  /usr/local/include
  /usr/include
  ${PROJECT_SOURCE_DIR}/include
  ./
  ./mv_json/include
)

#所依赖库的目录路径
LINK_DIRECTORIES(
	.
	../lib 
	/usr/local/lib
	/usr/lib64
	/usr/local/python3/lib
	${PROJECT_SOURCE_DIR}/lib
 )

set(CMAKE_CXX_FLAGS "-Wl,-rpath=. -Wl,-rpath-link=.")

ADD_SUBDIRECTORY(mv_json)

ADD_EXECUTABLE(mv_json_demo ${SOURCE_FILES})

#依赖的库文件
TARGET_LINK_LIBRARIES(mv_json_demo rt)
TARGET_LINK_LIBRARIES(mv_json_demo event)
TARGET_LINK_LIBRARIES(mv_json_demo pthread)
TARGET_LINK_LIBRARIES(mv_json_demo util)
TARGET_LINK_LIBRARIES(mv_json_demo dl)
TARGET_LINK_LIBRARIES(mv_json_demo mvjson)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
