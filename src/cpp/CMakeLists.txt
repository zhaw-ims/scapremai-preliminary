cmake_minimum_required(VERSION 2.8)
project(scapremai-preliminary CXX)

add_definitions("-std=c++11")

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()


add_executable(scapremai_sampler scapremai/sampler.cpp)
target_link_libraries(scapremai_sampler ${CONAN_LIBS})