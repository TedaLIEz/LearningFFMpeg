project(LearningFFMpeg)

cmake_minimum_required(VERSION 2.8)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/CMakeModules)

# set default flags values for all projects
# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
# set(CMAKE_C_FLAGS_RELEASE "-w -Os -fomit-frame-pointer ${CMAKE_C_FLAGS_RELEASE}")
# set(CMAKE_C_FLAGS_DEBUG "-Wall -O0 -g -DDEBUG ${CMAKE_C_FLAGS_DEBUG}")
set(CMAKE_CXX_FLAGS ${CMAKE_C_FLAGS})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
# set(CMAKE_CXX_FLAGS_RELEASE ${CMAKE_C_FLAGS_RELEASE})
# set(CMAKE_CXX_FLAGS_DEBUG ${CMAKE_C_FLAGS_DEBUG})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -D__LIBAVRESAMPLE__ -std=c99")

add_executable(LearningFFMpeg tutorial1.c)

include_directories(".")
find_package(FFmpeg REQUIRED)

# FFMPEG_FOUND - system has ffmpeg or libav
# FFMPEG_INCLUDE_DIR - the ffmpeg include directory
# FFMPEG_LIBRARIES 
# FFMPEG_LIBAVCODEC
# FFMPEG_LIBAVFORMAT
# FFMPEG_LIBAVUTIL
if (FFMPEG_FOUND)
    message("Found FFMPEG/LibAV libraries")
        message(${FFMPEG_LIBRARIES})
    include_directories(${FFMPEG_INCLUDE_DIR})
    target_link_libraries (LearningFFMpeg ${FFMPEG_LIBRARIES} "/usr/local/lib/libswscale.dylib" "/usr/local/opt/sdl/lib/libSDL-1.2.0.dylib")
else (FFMPEG_FOUND)
    message("Can't find libavcodec, libavformat or libavutil. Add them!")
endif (FFMPEG_FOUND)

target_link_libraries (LearningFFMpeg "-lm")
target_link_libraries (LearningFFMpeg "-lavresample")

