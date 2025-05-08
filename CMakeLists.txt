cmake_minimum_required(VERSION 3.20)

if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  set(CMAKE_TOOLCHAIN_FILE
      "C:/Users/Landorus/Desktop/vcpkg/scripts/buildsystems/vcpkg.cmake"
      CACHE STRING "Vcpkg toolchain file")
endif()

project(lob_alpha_engine
    VERSION 0.1.0
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include_directories(${PROJECT_SOURCE_DIR}/include)

file(GLOB_RECURSE LOB_SOURCES
    "${PROJECT_SOURCE_DIR}/src/*.cpp"
)

add_executable(${PROJECT_NAME}
    ${LOB_SOURCES}
)

# C++ arrow
find_package(Arrow REQUIRED)
# GoogleTest for unit tests
find_package(GTest REQUIRED)
# pybind11 for Python bindings
find_package(pybind11 REQUIRED)
# fmt for string formatting
find_package(fmt REQUIRED)
# spdlog for logging
find_package(spdlog REQUIRED)

# Link libs to main executable (add more as you need them)
target_link_libraries(${PROJECT_NAME} PRIVATE
    Arrow::arrow
    fmt::fmt
    spdlog::spdlog
)

# Enable testing and include the tests directory
enable_testing()
add_subdirectory(tests)
