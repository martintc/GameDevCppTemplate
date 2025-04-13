cmake_minimum_required(VERSION 3.16)
project(template) # replace

set(CMAKE_CXX_STANDARD 17)
find_package(OpenGL REQUIRED)

add_subdirectory(thirdparty/glfw)
include_directories(thirdparty/glfw/include)
add_subdirectory(thirdparty/glm)
# include_directories(thirdparty/glm/include)

set(GLAD ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/glad/src/glad.c ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/glad/include/glad/glad.h)

file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

set (COMPILATION_UNIT
  ${MY_SOURCES}
  ${GLAD})

add_executable("${CMAKE_PROJECT_NAME}" ${COMPILATION_UNIT})

set_property(TARGET "${CMAKE_PROJECT_NAME}" PROPERTY CXX_STANDARD 17)

target_sources("${CMAKE_PROJECT_NAME}" PRIVATE ${MY_SOURCES})

target_include_directories("${CMAKE_PROJECT_NAME}" PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include/")

target_link_libraries("${CMAKE_PROJECT_NAME}" PRIVATE glm glfw OpenGL::GL)
