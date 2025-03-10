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
set(SRC_DIR "${CMAKE_SOURCE_DIR}/src")

# Include directories for GLFW, GLAD, and source files
include_directories(
    ${GLFW_DIR}/include
    ${GLAD_DIR}/include
    ${SRC_DIR}
)

# Add GLFW as a subdirectory (if you want to build GLFW as part of the project)
add_subdirectory(${GLFW_DIR})

# Add Glad source file
set(GLAD_SOURCES ${GLAD_DIR}/src/glad.c)

# Automatically collect all .cpp files inside src/
file(GLOB SOURCE_FILES "${SRC_DIR}/*.cpp")

# Iterate over each .cpp file and create an executable
foreach(SRC_FILE ${SOURCE_FILES})
    # Extract filename without extension
    get_filename_component(EXECUTABLE_NAME ${SRC_FILE} NAME_WE)

    # Create an executable for each .cpp file
    add_executable(${EXECUTABLE_NAME} ${SRC_FILE} ${GLAD_SOURCES})

    # Link GLFW and OpenGL
    find_package(OpenGL REQUIRED)
    target_link_libraries(${EXECUTABLE_NAME} OpenGL::GL glfw)

    # Set platform-specific OpenGL linking
    if(WIN32)
        target_link_libraries(${EXECUTABLE_NAME} opengl32)
    elseif(APPLE)
        target_link_libraries(${EXECUTABLE_NAME} OpenGL)
    else()
        target_link_libraries(${EXECUTABLE_NAME} GL)
    endif()
endforeach()

# Specify the CMake binary directory for build output
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
