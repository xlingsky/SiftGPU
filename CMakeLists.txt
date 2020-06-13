CMAKE_MINIMUM_REQUIRED(VERSION 3.3)

PROJECT(SIFTGPU LANGUAGES CXX VERSION 1.2.0)

#SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -Wno-write-strings -Wno-unused-result -Wno-deprecated -fPIC")
#SET(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -Wno-write-strings -Wno-unused-result -Wno-deprecated -fPIC")

if(COMMAND cmake_policy)
    cmake_policy(SET CMP0042 NEW)
endif(COMMAND cmake_policy)

ADD_SUBDIRECTORY(src)

