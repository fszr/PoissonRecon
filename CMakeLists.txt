cmake_minimum_required(VERSION 3.10)

# 项目信息
project(PoissonRecon)

# 设置编译选项
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -DRELEASE -funroll-loops -ffast-math")
set(CMAKE_CXX_FLAGS_DEBUG "-DDEBUG -g3")

# 设置编译器选项
if(NOT DEFINED COMPILER)
    set(COMPILER gcc)
endif()

if(COMPILER STREQUAL "gcc")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fopenmp -Wno-deprecated -pthread -Wno-invalid-offsetof")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lgomp -lstdc++ -lpthread")
elseif(COMPILER STREQUAL "gcc-11")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fopenmp -Wno-deprecated -pthread -Wno-invalid-offsetof -Werror=strict-aliasing -Wno-nonnull")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lgomp -lstdc++ -lpthread")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated -std=c++17 -pthread -Wno-invalid-offsetof -Wno-dangling-else")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lstdc++")
endif()

find_package(Boost REQUIRED COMPONENTS system)
find_package(ZLIB REQUIRED)
find_package(PNG REQUIRED)
find_package(JPEG REQUIRED)

set(SRC_DIR ${CMAKE_SOURCE_DIR}/Src)
set(BIN_DIR ${CMAKE_BINARY_DIR}/Bin/Linux)

# 设置调试与发布目标
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_definitions(-DDEBUG)
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
    add_definitions(-DRELEASE)
endif()

add_subdirectory(Src)
