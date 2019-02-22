cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(SimpleTensor)

set(CMAKE_PREFIX_PATH "C:\\Libtorch")
find_package(Torch REQUIRED)

add_executable(SimpleTensor SimpleTensor.cpp)
target_link_libraries(SimpleTensor "${TORCH_LIBRARIES}")
set_property(TARGET SimpleTensor PROPERTY CXX_STANDARD 11)