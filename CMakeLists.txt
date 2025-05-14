cmake_minimum_required(VERSION 3.20)
project(lob_alpha_engine LANGUAGES CXX)

# ————————————————————————————————
# 1. C++ standard and toolchain
# ————————————————————————————————
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# If you’re using vcpkg for deps, point CMake to its toolchain file
if(EXISTS "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake")
  set(CMAKE_TOOLCHAIN_FILE
      "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
      CACHE STRING "Vcpkg toolchain file")
endif()

# ————————————————————————————————
# 2. Find dependencies
# ————————————————————————————————
# GoogleTest for unit tests
find_package(GTest CONFIG REQUIRED)

# (Optional) Apache Arrow if you’ll start on parquet/io in Week 2
# find_package(Arrow CONFIG REQUIRED)

# ————————————————————————————————
# 3. Declare targets
# ————————————————————————————————
# 3.1 Hello LOB demo
add_executable(hello_lob
  src/main.cpp
)
# (No extra libs for hello_lob)

# 3.2 Dummy test target
enable_testing()
add_executable(test_dummy
  tests/test_dummy.cpp
)
target_link_libraries(test_dummy
  PRIVATE
    GTest::gtest_main
)
add_test(
  NAME DummyTest
  COMMAND test_dummy
)

# ————————————————————————————————
# 4. (Future) include subdirectories
# ————————————————————————————————
# Later you can split into src/engine_core, src/data_pipeline, etc:
# add_subdirectory(src/engine_core)
# add_subdirectory(src/data_pipeline)
# add_subdirectory(tests)

# ————————————————————————————————
# 5. Installation rules (optional)
# ————————————————————————————————
# install(TARGETS hello_lob test_dummy
#         RUNTIME DESTINATION bin)

# ————————————————————————————————
# 6. Configure testing output
# ————————————————————————————————
# Make sure tests run verbose
set(CTEST_OUTPUT_ON_FAILURE ON)