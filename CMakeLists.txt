cmake_minimum_required(VERSION 3.17)
project(cpmsdlexample C)

set(CMAKE_C_STANDARD 11)

if (UNIX)
    set(CMAKE_BUILD_RPATH  $ORIGIN)
endif()

include(cmake/CPM.cmake)
CPMAddPackage(
        NAME SDL2
        VERSION 2.0.16
        URL https://www.libsdl.org/release/SDL2-2.0.16.zip
)

add_executable(cpmsdlexample main.c)
target_link_libraries(cpmsdlexample SDL2main SDL2)

IF (WIN32)
    message(STATUS "Detected Win32!")
    if (CMAKE_BUILD_TYPE STREQUAL "Debug")
        set(MY_SDL2_LIB_NAME "SDL2d.dll")
    ELSEIF(CMAKE_BUILD_TYPE STREQUAL "Release")
        set(MY_SDL2_LIB_NAME "SDL2.dll")
    ENDIF()
elseif(UNIX)
    message(STATUS "Detected Unix!")
    if (CMAKE_BUILD_TYPE STREQUAL "Debug")
        set(MY_SDL2_LIB_NAME "libSDL2-2.0d.so.0")
    ELSEIF(CMAKE_BUILD_TYPE STREQUAL "Release")
        set(MY_SDL2_LIB_NAME "libSDL2-2.0.so.0")
    ENDIF()
ENDIF()

if (MY_SDL2_LIB_NAME)
    message("copy from ${CMAKE_CURRENT_BINARY_DIR}/_deps/sdl2-build/${MY_SDL2_LIB_NAME} to ${CMAKE_CURRENT_BINARY_DIR}")
    add_custom_command(TARGET cpmsdlexample POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy
            "${CMAKE_CURRENT_BINARY_DIR}/_deps/sdl2-build/${MY_SDL2_LIB_NAME}"
            ${CMAKE_CURRENT_BINARY_DIR})
ENDIF()