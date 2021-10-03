cmake_minimum_required(VERSION 3.20)
project(cpmsdlexample C)

set(CMAKE_C_STANDARD 11)

include(cmake/CPM.cmake)
CPMAddPackage(
        NAME SDL2
        VERSION 2.0.16
        URL https://www.libsdl.org/release/SDL2-2.0.16.zip
)

add_executable(cpmsdlexample main.c)
target_link_libraries(cpmsdlexample SDL2)