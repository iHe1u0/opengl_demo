cmake_minimum_required(VERSION 3.26)

project(opengl_demo)

set(CMAKE_CXX_STANDARD 17)

include_directories(
        ${CMAKE_SOURCE_DIR}/
        ${CMAKE_SOURCE_DIR}/include/
        ${CMAKE_SOURCE_DIR}/src/
)

if (WIN32)
    if (MSVC)
        set(OPENGL_LIBRARY_PATH ${CMAKE_SOURCE_DIR}/lib/windows/msvc/)
    else ()
        set(OPENGL_LIBRARY_PATH ${CMAKE_SOURCE_DIR}/lib/windows/gcc/)
    endif ()
elseif (UNIX)
    set(OPENGL_LIBRARY_PATH ${CMAKE_SOURCE_DIR}/lib/linux/)
else ()
    message(FATAL_ERROR "Unsupported operating system")
endif()

find_library(OPENGL_LIBRARY glfw3 PATHS ${OPENGL_LIBRARY_PATH})

add_executable(opengl_demo src/main.cpp
        src/main.h
        src/glad.c
)

target_link_libraries(opengl_demo ${OPENGL_LIBRARY})
