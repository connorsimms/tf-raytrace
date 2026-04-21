cmake_minimum_required(VERSION 3.14)
project(taskflow_raytracer CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
    message(STATUS "Setting build type to 'Release' as none was specified.")
endif()

# ----- Taskflow -----
option(USE_TASKFLOW "Enable Taskflow parallelization" ON)

if(USE_TASKFLOW)
    find_package(Taskflow REQUIRED)
endif()
# --------------------

add_executable(raytracer main.cc)

target_include_directories(raytracer PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/src
)

target_compile_options(raytracer PRIVATE -O3)

if(USE_TASKFLOW)
    target_link_libraries(raytracer PRIVATE Taskflow::Taskflow)
    
    target_compile_definitions(raytracer PRIVATE USE_TASKFLOW)
endif()
