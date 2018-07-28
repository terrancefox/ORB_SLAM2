cmake_minimum_required(VERSION 2.8)
project(DBoW3)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -O3 -march=native")

set(HDRS_DBOW3
  src/BowVector.h
  src/FeatureVector.h
  src/ScoringObject.h   
  src/Vocabulary.h
  src/DBoW3.h
  src/Database.h
  src/DescManip.h
  src/QueryResults.h
  src/exports.h
  src/quicklz.h
  src/timers.h
  )
set(SRCS_DBOW3
  src/BowVector.cpp
  src/FeatureVector.cpp
  src/ScoringObject.cpp
  src/DescManip.cpp
  src/Database.cpp
  src/QueryResults.cpp
  src/quicklz.c
  src/Vocabulary.cpp
  )

set(OpenCV_DIR /usr/local/opencv3.2.0/share/OpenCV)
find_package(OpenCV 3.0 REQUIRED)
if(NOT OpenCV_FOUND)
   find_package(OpenCV 2.4.3 QUIET)
   if(NOT OpenCV_FOUND)
      message(FATAL_ERROR "OpenCV > 2.4.3 not found.")
   endif()
endif()

set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

include_directories(${OpenCV_INCLUDE_DIRS})
add_library(DBoW3 SHARED ${SRCS_DBOW3})
target_link_libraries(DBoW3 ${OpenCV_LIBS})
