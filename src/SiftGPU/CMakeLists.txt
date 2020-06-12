find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLEW)

set(SIFTGPU_VERSION 0.5.400)

SET(SIFTGPU_ENABLE_SERVER FALSE)
SET(SIFTGPU_ENABLE_OPENCL FALSE)
SET(SIFTGPU_ENABLE_CUDA FALSE)
SET(SIFTGPU_ENABLE_SSE TRUE)
SET(SIFTGPU_SSE_OPTIONS -march=core2 -mfpmath=sse)
SET(SIFTGPU_PREFER_GLUT TRUE)
SET(SIFTGPU_DISABLE_DEVIL TRUE)

if(UNIX)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -Wall -Wno-deprecated" )
else(UNIX)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_CRT_SECURE_NO_WARNINGS -DSIFTGPU_DLL -DDLL_EXPORT" )
  link_directories(Z:/repo/vcpkg/installed/x64-windows/lib)
endif(UNIX)

IF(SIFTGPU_ENABLE_SSE)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=core2 -mfpmath=sse" )
ENDIF(SIFTGPU_ENABLE_SSE)
  
IF(SIFTGPU_PREFER_GLUT)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DWINDOW_PREFER_GLUT" )
ENDIF(SIFTGPU_PREFER_GLUT)

IF(SIFTGPU_ENABLE_OPENCL)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DCL_SIFTGPU_ENABLED" )
ENDIF(SIFTGPU_ENABLE_OPENCL)

IF(APPLE)
  SET(LIBS_SIFTGPU )
ELSE(APPLE)
  #  SET(LIBS_SIFTGPU glut GL X11 )
ENDIF(APPLE)

IF(SIFTGPU_DISABLE_DEVIL)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSIFTGPU_NO_DEVIL" )
ELSE(SIFTGPU_DISABLE_DEVIL)
  SET(LIBS_SIFTGPU ${LIBS_SIFTGPU} IL )
ENDIF(SIFTGPU_DISABLE_DEVIL)

if (GLEW_FOUND)
	include_directories( ${GLEW_INCLUDE_DIRS} )
	SET (GLEW_LIBRARIES GLEW)
endif (GLEW_FOUND)

ADD_LIBRARY(siftgpu SHARED FrameBufferObject.cpp GlobalUtil.cpp GLTexImage.cpp ProgramGLSL.cpp 
            ProgramGPU.cpp ShaderMan.cpp SiftGPU.cpp SiftPyramid.cpp PyramidGL.cpp SiftMatch.cpp)

TARGET_LINK_LIBRARIES(siftgpu ${LIBS_SIFTGPU} ${GLEW_LIBRARIES} ${GLUT_LIBRARIES} ${OPENGL_LIBRARIES} )

SET_PROPERTY(TARGET siftgpu PROPERTY VERSION ${SIFTGPU_VERSION})

INSTALL(TARGETS siftgpu EXPORT siftgpuTargets
  LIBRARY DESTINATION lib 
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION  include
  )

INSTALL(FILES SiftGPU.h DESTINATION include)

#include(CMakePackageConfigHelpers)
#write_basic_package_version_file(
#  "${CMAKE_CURRENT_BINARY_DIR}/siftgpu/siftgpuConfigVersion.cmake"
#  VERSION ${SIFTGPU_VERSION}
#  COMPATIBILITY AnyNewerVersion
#)
#
#export(EXPORT siftgpuTargets
#  FILE "${CMAKE_CURRENT_BINARY_DIR}/siftgpu/siftgpuTargets.cmake"
#)
#configure_file(cmake/siftgpuConfig.cmake
#  "${CMAKE_CURRENT_BINARY_DIR}/siftgpu/siftgpuConfig.cmake"
#  COPYONLY
#)
#
#set(ConfigPackageLocation lib/cmake/siftgpu)
#install(EXPORT siftgpuTargets
#  FILE
#    siftgpuTargets.cmake
#  DESTINATION
#    ${ConfigPackageLocation}
#)
#install(
#  FILES
#    cmake/siftgpuConfig.cmake
#    "${CMAKE_CURRENT_BINARY_DIR}/siftgpu/siftgpuConfigVersion.cmake"
#  DESTINATION
#    ${ConfigPackageLocation}
#)
