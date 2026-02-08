cmake_minimum_required(VERSION 3.20)

project(BabaIsYou LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include(FetchContent)

FetchContent_Declare(
    raylib
    GIT_REPOSITORY https://github.com/raysan5/raylib.git
    GIT_TAG 6.0
    GIT_SHALLOW TRUE
)
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(BUILD_GAMES OFF CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(raylib)

set (SOURCES
    src/main.cpp
    src/game.cpp
    src/level.cpp
    src/tile.cpp

    src/bimap.h
    src/game.h
    src/level.h
    src/tile.h
)

add_executable(${PROJECT_NAME} ${SOURCES})

source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${SOURCES})

set_property(DIRECTORY ${CMAKE_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME} PRIVATE "src")

target_link_libraries(${PROJECT_NAME} PRIVATE raylib)
