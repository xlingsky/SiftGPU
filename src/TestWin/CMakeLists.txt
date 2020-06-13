find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLEW REQUIRED)

include_directories( ${GLEW_INCLUDE_DIRS} )

ADD_EXECUTABLE(SimpleSIFT SimpleSIFT.cpp)
TARGET_LINK_LIBRARIES(SimpleSIFT siftgpu)

find_package(glm)
IF(glm_FOUND)

if(UNIX)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-deprecated" )
else(UNIX)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_CRT_SECURE_NO_WARNINGS" )
endif(UNIX)
  ADD_EXECUTABLE(TestWinGlut TestWinGlut.cpp BasicTestWin.cpp )
  TARGET_LINK_LIBRARIES(TestWinGlut siftgpu)
ENDIF(glm_FOUND)

set(CMAKE_VERBOSE_MAKEFILE ON)
