cmake_minimum_required(VERSION 3.11)
project(OpenGLProject)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(FetchContent)

FetchContent_Declare(
  glfw
  GIT_REPOSITORY https://github.com/glfw/glfw.git
  GIT_TAG 3.4)

# GLFW options - disable unnecessary features
set(GLFW_BUILD_DOCS
    OFF
    CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS
    OFF
    CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES
    OFF
    CACHE BOOL "" FORCE)

# Make GLFW available
FetchContent_MakeAvailable(glfw)

# Find OpenGL package
find_package(OpenGL REQUIRED)

# Create executable
add_executable(hello_triangle src/main.cpp external/glad/src/glad.c)

# Add include directories
target_include_directories(hello_triangle PRIVATE external/glad/include)

# Link libraries
target_link_libraries(
  hello_triangle glfw OpenGL::GL ${CMAKE_DL_LIBS} # For dlopen/dlsym
)

# Linux-specific libraries
if(UNIX AND NOT APPLE)
  target_link_libraries(hello_triangle X11 pthread Xrandr Xi)
endif()
