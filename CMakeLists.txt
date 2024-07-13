cmake_minimum_required(VERSION 3.10)
project(MyProject)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 添加头文件目录
include_directories(${CMAKE_SOURCE_DIR})

# 查找需要的框架
find_library(FOUNDATION_FRAMEWORK Foundation)
find_library(COREML_FRAMEWORK CoreML)
find_library(ACCELERATE_FRAMEWORK Accelerate)

# 添加源文件
set(SOURCE_FILES
        main.cpp
        objcWrapper.mm
        coreml/CoremlEncoder.m
        )

# 添加目标
add_executable(main ${SOURCE_FILES})

# 链接框架
target_link_libraries(main
        ${FOUNDATION_FRAMEWORK}
        ${COREML_FRAMEWORK}
        ${ACCELERATE_FRAMEWORK}
        )

# 设置 Objective-C++ 编译器标志
set_source_files_properties(objcWrapper.mm PROPERTIES COMPILE_FLAGS "-fobjc-arc")
set_source_files_properties(coreml/CoremlEncoder.m PROPERTIES COMPILE_FLAGS "-fobjc-arc")