```cmake
cmake_minimum_required(VERSION 3.21)

project(HighGraphics VERSION 1.2.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)

# Find Geode SDK
if (NOT DEFINED ENV{GEODE_SDK})
    message(FATAL_ERROR
        "Unable to find Geode SDK! Please define GEODE_SDK environment variable."
    )
endif()

message(STATUS "Found Geode: $ENV{GEODE_SDK}")

# Add Geode SDK first
add_subdirectory(
    "$ENV{GEODE_SDK}"
    "${CMAKE_CURRENT_BINARY_DIR}/geode"
)

# Source files
file(GLOB_RECURSE SOURCES
    src/*.cpp
)

# Mod library
add_library(${PROJECT_NAME} SHARED ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE
    include
)

# Setup Geode mod
setup_geode_mod(${PROJECT_NAME})
```
