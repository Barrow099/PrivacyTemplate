cmake_minimum_required(VERSION 3.14)
project(Solution)

set(SQLITE_SOURCES Lib/sqlite/sqlite3.c)
include_directories(Lib/sqlite)

add_subdirectory(Lib/armadillo-10.4.0)


if(WIN32)

else()
    find_package(Threads)
endif()

set(CMAKE_CXX_STANDARD 14)



add_executable(Solution main.cpp ${SQLITE_SOURCES})
target_link_directories(Solution PUBLIC Lib/faszom)
if(MSVC)
    target_link_libraries(Solution armadillo liblapack libblas)
elseif(WIN32)
    target_link_libraries(Solution armadillo lapack blas)
else()
    target_link_libraries(Solution armadillo Threads::Threads dl m lapack blas)
endif()
