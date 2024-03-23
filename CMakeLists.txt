cmake_minimum_required(VERSION 3.22)
project(cparse LANGUAGES CXX)

SET(
    ${PROJECT_NAME}_SOURCES
    builtin-features.cpp
    containers.cpp
    functions.cpp
    packToken.cpp
    shunting-yard.cpp
)

SET(${PROJECT_NAME}_HEADERS
    containers.h
    functions.h
    packToken.h
    shunting-yard.h
    shunting-yard-exceptions.h
)

add_library(${PROJECT_NAME} STATIC)
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})
target_sources(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${${PROJECT_NAME}_SOURCES}> )

target_compile_definitions(${PROJECT_NAME} INTERFACE CPARSE_ENABLE_CPARSE)

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:cparse>
)
set_property(TARGET ${PROJECT_NAME}
 PROPERTY PUBLIC_HEADER ${${PROJECT_NAME}_HEADERS})

install(TARGETS  ${PROJECT_NAME}
INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}" 
)
