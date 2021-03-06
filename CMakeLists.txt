cmake_minimum_required(VERSION 3.9.2)
project(ray-tracer)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

find_package(SFML REQUIRED system window graphics)

include_directories(${SFML_INCLUDE_DIR})

set(RAY_TRACER_SOURCES
  src/main.cpp)

set(RAY_TRACER_HEADERS
  color.hpp
  mat4x4.hpp
  vec.hpp)

add_executable(ray-tracer ${RAY_TRACER_SOURCES})

set_target_properties(ray-tracer PROPERTIES
  CXX_STANDARD 17)

target_compile_options(ray-tracer PRIVATE
  -Wall
  -Werror
  -Wconversion
  -Wno-missing-braces
  -Wunused-variable
  -pedantic)

target_link_libraries(ray-tracer ${SFML_LIBRARIES})

include(CppLint)
add_cpp_lint_target(lint ${RAY_TRACER_SOURCES} ${RAY_TRACER_HEADERS})
add_dependencies(ray-tracer lint)
