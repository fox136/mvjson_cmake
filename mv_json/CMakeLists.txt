
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
FILE(GLOB_RECURSE SOURCE_FILES ${PROJECT_SOURCE_DIR}/src/*.cpp)   


#相关头文件的目录    
INCLUDE_DIRECTORIES( 
  /usr/include/c++/6.1.0
  /usr/local/include
  /usr/include
  ${PROJECT_SOURCE_DIR}/include
  ./
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

#ADD_LIBRARY(mvjson ${SOURCE_FILES})  # 静态库
ADD_LIBRARY(mvjson SHARED ${SOURCE_FILES})  # 动态库

#依赖的库文件
TARGET_LINK_LIBRARIES(mvjson rt)
TARGET_LINK_LIBRARIES(mvjson event)
TARGET_LINK_LIBRARIES(mvjson pthread)
TARGET_LINK_LIBRARIES(mvjson util)
TARGET_LINK_LIBRARIES(mvjson dl)

SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
