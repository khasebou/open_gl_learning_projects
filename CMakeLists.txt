cmake_minimum_required(VERSION 3.9)
project(ptg)


#GLFW additions
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
# Disable on Solus OS budgie desktop doesn't support wayland
set(GLFW_BUILD_WAYLAND OFF CACHE BOOL "" FORCE)

add_subdirectory(lib/glfw)
include_directories(lib/glad/include)
include_directories(lib/glfw)
include_directories(lib/glfw/deps)
include_directories(lib/glfw/include)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/build)
set(GLAD "${CMAKE_CURRENT_SOURCE_DIR}/lib/glad/include/glad/glad.h"
         "${CMAKE_CURRENT_SOURCE_DIR}/lib/glad/src/glad.c")
set(GETOPT "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/deps/getopt.h"
           "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/deps/getopt.c")
set(TINYCTHREAD "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/deps/tinycthread.h"
                "${CMAKE_CURRENT_SOURCE_DIR}/lib/glfw/deps/tinycthread.c")

set(SOURCE_FILES src/main.cpp)

add_executable(main ${SOURCE_FILES} ${TINYCTHREAD} ${GETOPT} ${GLAD})

file(COPY shaders DESTINATION build)

target_link_libraries(main glfw ${GLFW_LIBRARIES})