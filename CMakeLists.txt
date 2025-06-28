cmake_minimum_required(VERSION 3.14)
project(YOLOv8Detector)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")

# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# ONNX Runtime
include_directories(/usr/local/include/onnxruntime)

find_library(ONNXRUNTIME_LIBRARY NAMES onnxruntime PATHS /usr/local/lib)
if(NOT ONNXRUNTIME_LIBRARY)
    message(FATAL_ERROR "onnxruntime library not found in /usr/local/lib")
endif()

add_executable(${PROJECT_NAME} ../detector.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE ${OpenCV_LIBS} ${ONNXRUNTIME_LIBRARY})