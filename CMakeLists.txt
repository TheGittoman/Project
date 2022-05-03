cmake_minimum_required(VERSION 3.0.0)
project(Project VERSION 0.1.0)

include(CTest)
enable_testing()

add_executable(${PROJECT_NAME} main.cpp)

add_subdirectory(src)

add_subdirectory(external/glfw)

add_subdirectory(external/imgui)

target_include_directories(${PROJECT_NAME} 
  PUBLIC src
  PUBLIC external/glfw/include
  PUBLIC external/imgui
)

target_link_directories(${PROJECT_NAME} 
  PRIVATE src
  PRIVATE external/glfw/src
  PRIVATE external/imgui
)

target_link_libraries(${PROJECT_NAME} header glfw IMGUI opengl32)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
