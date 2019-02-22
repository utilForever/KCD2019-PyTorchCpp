cmake_minimum_required(VERSION 3.1 FATAL_ERROR)
project(MNIST)

set(CMAKE_PREFIX_PATH "C:\\Libtorch")
find_package(Torch REQUIRED)

option(DOWNLOAD_MNIST "Download the MNIST dataset from the internet" ON)
if (DOWNLOAD_MNIST)
  message(STATUS "Downloading MNIST dataset")
  execute_process(
    COMMAND python ${CMAKE_CURRENT_LIST_DIR}/../Tools/download_mnist.py
      -d ${CMAKE_BINARY_DIR}/data
    ERROR_VARIABLE DOWNLOAD_ERROR)
  if (DOWNLOAD_ERROR)
    message(FATAL_ERROR "Error downloading MNIST dataset: ${DOWNLOAD_ERROR}")
  endif()
endif()

add_executable(MNIST MNIST.cpp)
target_compile_features(MNIST PUBLIC cxx_range_for)
target_link_libraries(MNIST ${TORCH_LIBRARIES})