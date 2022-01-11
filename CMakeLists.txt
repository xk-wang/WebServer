cmake_minimum_required(VERSION 3.16)

project(server)
set(CMAKE_BUILD_TYPE RELEASE)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -O2 -Wall -g")
# /usr/bin/mysql_config
set(MYSQL_LIBS mysqlclient pthread)

file(GLOB_RECURSE LOG code/log/*.cpp)
file(GLOB_RECURSE POOL code/pool/*.cpp)
file(GLOB_RECURSE TIMER code/timer/*.cpp)
file(GLOB_RECURSE HTTP code/http/*.cpp)
file(GLOB_RECURSE SERVER code/server/*.cpp)
file(GLOB_RECURSE BUFFER code/buffer/*.cpp)

add_executable(server ${LOG} ${POOL} ${TIMER} ${HTTP} ${SERVER} ${BUFFER} code/main.cpp)
target_include_directories(server PRIVATE /usr/include/)
target_link_directories(server PRIVATE /usr/lib/mysql/plugin)
target_link_directories(server PRIVATE /usr/lib/x86_64-linux-gnu)
target_link_libraries(server PRIVATE ${MYSQL_LIBS})