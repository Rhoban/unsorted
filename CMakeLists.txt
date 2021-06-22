cmake_minimum_required(VERSION 3.16.3)
project(rhoban_unsorted)

include_directories(include ${catkin_INCLUDE_DIRS})

#Enable C++17
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -Wall -Wextra")

#Enable Weird option linker
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")

#List Sources sub source directories
set(SOURCES_DIRECTORIES
  src/rhoban_unsorted
)

#Include Sources sub sources
foreach (DIRECTORY ${SOURCES_DIRECTORIES})
    message(STATUS "-- Sources: Adding ${DIRECTORY}/")
    include (${DIRECTORY}/Sources.cmake)
    set (PREFIXED_SOURCES)
    foreach (SOURCE ${SOURCES})
        set (PREFIXED_SOURCES ${PREFIXED_SOURCES} ${DIRECTORY}/${SOURCE})
    endforeach (SOURCE)
    set (ALL_SOURCES ${ALL_SOURCES} ${PREFIXED_SOURCES})
endforeach (DIRECTORY)

add_library (rhoban_unsorted ${ALL_SOURCES})
target_link_libraries(rhoban_unsorted PUBLIC rhoban_utils)
target_include_directories(rhoban_unsorted PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)
