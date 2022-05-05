cmake_minimum_required(VERSION 3.23)
project(Project VERSION 1.0)

include(CTest)
enable_testing()

add_executable(${PROJECT_NAME} main.cpp)

# use logic
option(USE_HEADER "Toggle this unnecessary thing off" ON)
if(USE_HEADER)
  add_subdirectory(src)
  list(APPEND EXTRA_LIBS header)
  list(APPEND EXTRA_INCLUDES ${PROJECT_SOURCE_DIR}/src)
endif()

# adds configure file that builds in /build directory as ProjectConfig.h
configure_file(ProjectConfig.h.in ProjectConfig.h)


add_subdirectory(external/glfw)

add_subdirectory(external/imgui)

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})

target_include_directories(${PROJECT_NAME} 
  PUBLIC external/glfw/include
  PUBLIC external/imgui
  ${EXTRA_INCLUDES}
)

target_link_directories(${PROJECT_NAME} 
  PRIVATE external/glfw/src
  PRIVATE external/imgui
)


target_link_libraries(${PROJECT_NAME} ${EXTRA_LIBS} glfw imgui opengl32)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
