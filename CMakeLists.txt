cmake_minimum_required(VERSION 3.20)
project(lob_alpha_engine LANGUAGES CXX)

# ————————————————————————————————
# 1. C++ standard
# ————————————————————————————————
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ————————————————————————————————
# 2. Fetch GoogleTest via FetchContent
# ————————————————————————————————
include(FetchContent)
FetchContent_Declare(
  googletest
  URL  https://github.com/google/googletest/archive/release-1.17.0.zip
)
# For Windows: prevent overriding our compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

# ————————————————————————————————
# 3. Arrow (AUR) and other dependencies
# ————————————————————————————————
find_package(Arrow CONFIG REQUIRED)

# ————————————————————————————————
# 4. Targets
# ————————————————————————————————
add_executable(hello_lob src/main.cpp)

enable_testing()
add_executable(test_dummy tests/test_dummy.cpp)
target_link_libraries(test_dummy PRIVATE gtest_main)
add_test(NAME DummyTest COMMAND test_dummy)

set(CTEST_OUTPUT_ON_FAILURE ON)