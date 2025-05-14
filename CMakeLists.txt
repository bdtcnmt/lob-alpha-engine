cmake_minimum_required(VERSION 3.20)
project(lob_alpha_engine LANGUAGES CXX)

# ————————————————————————————————
# 1. C++ standard
# ————————————————————————————————
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ————————————————————————————————
# 2. GoogleTest (vendored submodule)
# ————————————————————————————————
# Assumes you did: git submodule add https://github.com/google/googletest.git extern/googletest
add_subdirectory(extern/googletest)

# ————————————————————————————————
# 3. System dependencies
# ————————————————————————————————
# Apache Arrow (installed via AUR: arrow-cpp, parquet-cpp)
find_package(Arrow CONFIG REQUIRED)

# ————————————————————————————————
# 4. Define targets
# ————————————————————————————————
# 4.1 Hello LOB demo
add_executable(hello_lob
  src/main.cpp
)

# 4.2 Dummy test
enable_testing()
add_executable(test_dummy
  tests/test_dummy.cpp
)
target_link_libraries(test_dummy
  PRIVATE
    gtest_main
)
add_test(
  NAME DummyTest
  COMMAND test_dummy
)

# ————————————————————————————————
# 5. Test output settings
# ————————————————————————————————
# Show full output on failure
set(CTEST_OUTPUT_ON_FAILURE ON)