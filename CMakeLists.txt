cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

set (PICO_SDK_FETCH_FROM_GIT ON)
include(pico_sdk_import.cmake)

#### compile_commands.json generation ####

set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

#### project settings ####

project         (rpi-pico-test)
set_property    (GLOBAL PROPERTY USE_FOLDERS ON)
set             (CMAKE_BUILD_TYPE Debug)
set             (CMAKE_C_STANDARD 17)

add_compile_options(-Wall -Wextra -pedantic -g)

#### project files ####

file(GLOB_RECURSE PROJECT_SOURCES src/*.c)

set(PROJECT_INCLUDE_DIRS
    ${PROJECT_INCLUDE_DIRS}
    src/)

#### project libraries ####

pico_sdk_init()
set(PROJECT_LIBRARIES ${PROJECT_LIBRARIES} pico_stdlib)

#### targets ####

add_executable              (${PROJECT_NAME} ${PROJECT_SOURCES})
pico_add_extra_outputs      (${PROJECT_NAME})

target_include_directories  (${PROJECT_NAME} PUBLIC ${PROJECT_INCLUDE_DIRS})
target_link_libraries       (${PROJECT_NAME} PUBLIC ${PROJECT_LIBRARIES})
target_compile_definitions  (${PROJECT_NAME} PUBLIC ${PROJECT_COMPILE_DEFINITIONS})
target_compile_options      (${PROJECT_NAME} PUBLIC ${PROJECT_COMPILE_OPTIONS})
set_target_properties       (${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE C)

