cmake_minimum_required(VERSION 3.21)

project(HighGraphicsonAndroid VERSION 1.2.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)

# Geode SDK
if (NOT DEFINED ENV{GEODE_SDK})
    message(FATAL_ERROR
        "GEODE_SDK environment variable is not set."
    )
endif()

message(STATUS "Using Geode SDK: $ENV{GEODE_SDK}")

# Load Geode SDK
add_subdirectory(
    "$ENV{GEODE_SDK}"
    "${CMAKE_BINARY_DIR}/geode"
)

# Sources
file(GLOB_RECURSE SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)

# Mod library
add_library(
    ${PROJECT_NAME}
    SHARED
    ${SOURCES}
)

# Headers
target_include_directories(
    ${PROJECT_NAME}
    PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

# Geode configuration
setup_geode_mod(${PROJECT_NAME})
