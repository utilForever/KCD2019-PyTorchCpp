cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(DCGAN)

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

add_executable(DCGAN DCGAN.cpp)
target_link_libraries(DCGAN "${TORCH_LIBRARIES}")
set_property(TARGET DCGAN PROPERTY CXX_STANDARD 11)