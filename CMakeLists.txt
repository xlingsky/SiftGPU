CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

PROJECT(SIFTGPU C CXX)

#SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -Wno-write-strings -Wno-unused-result -Wno-deprecated -fPIC")
#SET(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -Wno-write-strings -Wno-unused-result -Wno-deprecated -fPIC")
if (APPLE)
   set(CMAKE_MACOSX_RPATH ON)
endif (APPLE)
ADD_SUBDIRECTORY(src)

