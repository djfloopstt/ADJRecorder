cmake_minimum_required (VERSION 2.6)
project (ADJRecorder)

include(CheckCXXCompilerFlag)

set(CMAKE_BUILD_TYPE Debug)

# setup our include directories
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/src
  )

# setup our source files
set(SOURCE
    ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/src/RtMidi.cpp
  )

# setup our exe
add_executable(ADJRecorder ${SOURCE})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lua/include)

# setup MIDI stuff
find_library(COREMIDI_LIBRARY CoreMIDI)
find_library(COREAUDIO_LIBRARY CoreAudio)
find_library(COREFOUNDATION_LIBRARY CoreFoundation)

add_definitions(-D__MACOSX_CORE__)

target_link_libraries(ADJRecorder ${COREMIDI_LIBRARY} ${COREAUDIO_LIBRARY} ${COREFOUNDATION_LIBRARY})

# do tests for c++11 and c++14
if (CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR CMAKE_CXX_COMPILER_ID MATCHES "GNU")
  CHECK_CXX_COMPILER_FLAG("-std=c++14" HAS_CPP14_FLAG)
  CHECK_CXX_COMPILER_FLAG("-std=c++11" HAS_CPP11_FLAG)

  if (HAS_CPP14_FLAG)
      set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")
  elseif (HAS_CPP11_FLAG)
      set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  else()
      message(FATAL_ERROR "Unsupported compiler -- at least C++11 support is needed!")
  endif()
endif()

# copy binary to root after build
add_custom_command(TARGET ADJRecorder POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:ADJRecorder> $<TARGET_FILE_DIR:ADJRecorder>/../ADJRecorder
)
