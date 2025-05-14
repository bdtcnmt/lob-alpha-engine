cmake_minimum_required(VERSION 3.20)
project(lob_alpha_engine LANGUAGES CXX)

# ————————————————————————————————
# 1. C++ standard
# ————————————————————————————————
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ————————————————————————————————
# 2. Dependencies
# ————————————————————————————————
# GoogleTest for unit tests
find_package(GTest CONFIG REQUIRED)

# Apache Arrow (installed from AUR: arrow-cpp, parquet-cpp)
find_package(Arrow CONFIG REQUIRED)

# ————————————————————————————————
# 3. Targets
# ————————————————————————————————
# 3.1 Hello LOB demo
add_executable(hello_lob
  src/main.cpp
)

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
# 4. Future modules
# ————————————————————————————————
# Later you can split into subdirectories:
# add_subdirectory(src/engine_core)
# add_subdirectory(src/data_pipeline)
# add_subdirectory(tests)

# ————————————————————————————————
# 5. Configure test output
# ————————————————————————————————
# Show full output on test failure
set(CTEST_OUTPUT_ON_FAILURE ON)