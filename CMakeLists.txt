cmake_minimum_required(VERSION 3.5)

project(_Vision_ LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(ExternalProject)

ExternalProject_Add(
    fastcgipp
    PREFIX              ${CMAKE_CURRENT_SOURCE_DIR}/external
    GIT_REPOSITORY      https://github.com/eddic/fastcgipp.git
    INSTALL_COMMAND     ""
)

find_package(Boost REQUIRED)

find_package (PostgreSQL REQUIRED)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/external/src/fastcgipp/include
    ${CMAKE_CURRENT_SOURCE_DIR}/external/src/fastcgipp-build/include
    ${Boost_INCLUDE_DIR}
    ${PostgreSQL_INCLUDE_DIRS}
)

add_executable(_Vision_ main.cpp)

target_link_libraries(_Vision_
    ${CMAKE_CURRENT_SOURCE_DIR}/external/src/fastcgipp-build/libfastcgipp.so
    ${PostgreSQL_LIBRARIES})
