# Set the minimum required CMake version
cmake_minimum_required(VERSION 3.10)

# Project Name
project(OpenGL_Project)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Set paths to GLFW and GLAD
set(GLFW_DIR "${CMAKE_SOURCE_DIR}/glfw")
set(GLAD_DIR "${CMAKE_SOURCE_DIR}/glad")

# Include directories for GLFW and GLAD
include_directories(
    ${GLFW_DIR}/include
    ${GLAD_DIR}/include
)

# Add GLFW as a subdirectory (if you want to build GLFW as part of the project)
add_subdirectory(${GLFW_DIR})

# Add Glad source file
set(GLAD_SOURCES ${GLAD_DIR}/src/glad.c)

# Set source files
set(SOURCES
    triangle.cpp  # Replace with your source files
    ${GLAD_SOURCES}
)

# Create executable
add_executable(OpenGL_Project ${SOURCES})

# Link GLFW and OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(OpenGL_Project OpenGL::GL glfw)

# Set CMake options for GLFW (adjust paths if needed)
# Optionally, you can add these flags to link OpenGL libraries
if(WIN32)
    target_link_libraries(OpenGL_Project opengl32)
elseif(APPLE)
    target_link_libraries(OpenGL_Project OpenGL)
else()
    target_link_libraries(OpenGL_Project GL)
endif()

# Specify the CMake binary directory for build output
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)

# Create build directory and configure the build files
