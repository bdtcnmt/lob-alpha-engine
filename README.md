# Simulated LOB Alpha Engine & Visualizer

Repo 

## Project Overview

-**Phase 1**: High-performance C++23 LOB Simulator

-**Phase 2**: 3D dashboards for order-book and volatility surfaces

## Prerequisites

- CMake 3.20+
- A C++23-capable compiler (GCC/Clang)
- vcpkg or Conan for C++ dependencies
- Python 3.10+ and pip (for data tools and visualizer)

## Quickstart

```bash
# Clone the repo
$ git clone
$ cd lob-alpha-engine

# Create a build directory and build
$ mkdir build && cd build
$ cmake ..
$ cmake --build .

# Run the dummy test
$ ctest
```

## Project Layout

├── CMakeLists.txt       
├── README.md            
├── docs/                
├── src/                 
├── tests/               
└── .github/
