cmake_minimum_required(VERSION 3.14)
project(Solution)

set(SQLITE_SOURCES Lib/sqlite/sqlite3.c)
include_directories(Lib/sqlite)

add_subdirectory(Lib/armadillo-10.4.0)

if(MSVC)

else()
    find_package(Threads)
endif()

set(CMAKE_CXX_STANDARD 14)



add_executable(Solution main.cpp ${SQLITE_SOURCES})
if(MSVC)
    target_link_libraries(Solution armadillo)
else()
    target_link_libraries(Solution armadillo Threads::Threads dl m)
endif()