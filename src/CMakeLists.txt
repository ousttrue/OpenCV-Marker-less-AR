CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(OpenCVMarkerLessAR) # .sln

FIND_PACKAGE(OpenCV REQUIRED)
MESSAGE(STATUS ${OpenCV_INCLUDE_DIRS})

FIND_PACKAGE(OpenGL REQUIRED)
MESSAGE(STATUS ${OPENGL_LIBRARIES})
FIND_PACKAGE(GLUT)
MESSAGE(STATUS ${GLUT_LIBRARY})
STRING(REPLACE lib/freeglut.lib debug/lib/freeglutd.lib GLUT_LIBRARY_DEBUG ${GLUT_LIBRARY})
SET(OPENGL_LIBS 
    general ${OPENGL_LIBRARIES} 
    optimized ${GLUT_LIBRARY} 
    debug ${GLUT_LIBRARY_DEBUG}
    )

FIND_PACKAGE(PNG REQUIRED)
MESSAGE(STATUS ${PNG_LIBRARY})

##############################################################################
FILE(GLOB SRCS
    Main/*.cpp
    Main/*.h
    ObjRecog/*.cpp
    ObjRecog/*.h
    Overlay/*.cpp
    Overlay/*.c
    Overlay/*.h
    Tracking/*.cpp
    Tracking/*.h
    )
#MESSAGE(STATUS ${SRCS})
SET(CMAKE_CXX_FLAGS "/wd4819 /EHsc")
INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_SOURCE_DIR}/Main
    ${CMAKE_CURRENT_SOURCE_DIR}/ObjRecog
    ${CMAKE_CURRENT_SOURCE_DIR}/Tracking
    ${CMAKE_CURRENT_SOURCE_DIR}/Overlay
    ${CMAKE_INSTALL_PREFIX}/include
    ${OpenCV_INCLUDE_DIRS}
    )
ADD_EXECUTABLE(OpenCVMarkerLessAR 
    ${SRCS}
    )
TARGET_LINK_LIBRARIES(OpenCVMarkerLessAR
    ${OPENGL_LIBS}
    ${OpenCV_LIBRARIES}
    ${PNG_LIBRARY}
    )

