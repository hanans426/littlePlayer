﻿# CMakeList.txt : CMake project for FFmpegCMake, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("littlePlayer" VERSION 0.2.0)

# --------------------------------------------------------------------------
# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_FLAGS "-D__STDC_CONSTANT_MACROS")

IF(MSVC)
    SET(CMAKE_CXX_FLAGS "/EHsc")  # deal with MSVC Warning C4530
ENDIF(MSVC)




include(./.SET_LOCAL_PATH.cmake)
#----------------------------------------------
#  Content in my '.SET_LOCAL_PATH.cmake' file.
#----------------------------------------------
#set(CMAKE_INCLUDE_PATH 
#	"C:/tools/ffmpeg-4.2.2/include"
#	"C:/tools/SDL2-2.0.10/include"
#	"C:/Program Files (x86)/OpenAL 1.1 SDK/include"
#)
#
#set(CMAKE_LIBRARY_PATH 
#	"C:/tools/ffmpeg-4.2.2/lib"
#	"C:/tools/SDL2-2.0.10/lib"
#	"C:/Program Files (x86)/OpenAL 1.1 SDK/libs/Win64"
#)




######################################
#  FFmpeg lib setting
######################################
#make sure ffmpeg/bin is in your PATH to RUN.

find_path(AVCODEC_INCLUDE_DIR libavcodec/avcodec.h)
find_library(AVCODEC_LIBRARY avcodec)

find_path(AVFORMAT_INCLUDE_DIR libavformat/avformat.h)
find_library(AVFORMAT_LIBRARY avformat)

find_path(AVUTIL_INCLUDE_DIR libavutil/avutil.h)
find_library(AVUTIL_LIBRARY avutil)

find_path(AVDEVICE_INCLUDE_DIR libavdevice/avdevice.h)
find_library(AVDEVICE_LIBRARY avdevice)

find_path(AVFILTER_INCLUDE_DIR libavfilter/avfilter.h)
find_library(AVFILTER_LIBRARY avfilter)

find_path(POSTPROC_INCLUDE_DIR libpostproc/postprocess.h)
find_library(POSTPROC_LIBRARY postproc)

find_path(SWRESAMPLE_INCLUDE_DIR libswresample/swresample.h)
find_library(SWRESAMPLE_LIBRARY swresample)

find_path(SWSCALE_INCLUDE_DIR libswscale/swscale.h)
find_library(SWSCALE_LIBRARY swscale)




######################################
#  SDL2 lib setting
######################################
#make sure SDL2.dll is in your PATH.

# set(SDL_INCLUDE_DIR "C:/tools/SDL2-2.0.10/include")
# set(SDL_LIBRARY "C:/tools/SDL2-2.0.10/lib/x64/SDL2.lib")

find_path(SDL_INCLUDE_DIR "SDL2/SDL.h")
find_library(SDL_LIBRARY SDL2.lib)





######################################
#  OpenAL lib setting
######################################
#make sure openAL32.dll is in your PATH.

#set(OpenAL_INCLUDE_DIR "C:/Program Files (x86)/OpenAL 1.1 SDK/include")
#set(OpenAL_LIBRARY "C:/Program Files (x86)/OpenAL 1.1 SDK/libs/Win64/OpenAL32.lib")

find_path(OpenAL_INCLUDE_DIR "OpenAL/al.h")
find_library(OpenAL_LIBRARY "OpenAL32.lib")



######################################
#  information
######################################

message(CMAKE_SOURCE_DIR=${CMAKE_SOURCE_DIR})
message(PROJECT_SOURCE_DIR=${PROJECT_SOURCE_DIR})

message("--------------------")
message(CMAKE_INCLUDE_PATH=${CMAKE_INCLUDE_PATH})
message(CMAKE_LIBRARY_PATH=${CMAKE_LIBRARY_PATH})
message(CMAKE_PREFIX_PATH=${CMAKE_PREFIX_PATH})



message("--------------------")
message("FFMPEG INFORMATION")
message("--------------------")
message(AVCODEC_INCLUDE_DIR=${AVCODEC_INCLUDE_DIR})
message(AVCODEC_LIBRARY=${AVCODEC_LIBRARY})
message("--------------------")
message(AVFORMAT_INCLUDE_DIR=${AVFORMAT_INCLUDE_DIR})
message(AVFORMAT_LIBRARY=${AVFORMAT_LIBRARY})
message("--------------------")
message(AVUTIL_INCLUDE_DIR=${AVUTIL_INCLUDE_DIR})
message(AVUTIL_LIBRARY=${AVUTIL_LIBRARY})
message("--------------------")
message(AVDEVICE_INCLUDE_DIR=${AVDEVICE_INCLUDE_DIR})
message(AVDEVICE_LIBRARY=${AVDEVICE_LIBRARY})
message("--------------------")
message(AVFILTER_INCLUDE_DIR=${AVFILTER_INCLUDE_DIR})
message(AVFILTER_LIBRARY=${AVFILTER_LIBRARY})
message("--------------------")
message(POSTPROC_INCLUDE_DIR=${POSTPROC_INCLUDE_DIR})
message(POSTPROC_LIBRARY=${POSTPROC_LIBRARY})
message("--------------------")
message(SWRESAMPLE_INCLUDE_DIR=${SWRESAMPLE_INCLUDE_DIR})
message(SWRESAMPLE_LIBRARY=${SWRESAMPLE_LIBRARY})
message("--------------------")
message(SWSCALE_INCLUDE_DIR=${SWSCALE_INCLUDE_DIR})
message(SWSCALE_LIBRARY=${SWSCALE_LIBRARY})
message("--------------------")
message(SDL_INCLUDE_DIR=${SDL_INCLUDE_DIR})
message(SDL_LIBRARY=${SDL_LIBRARY})
message("--------------------")
message(OpenAL_INCLUDE_DIR=${OpenAL_INCLUDE_DIR})
message(OpenAL_LIBRARY=${OpenAL_LIBRARY})


############################################
# Add source to this project's executable.
############################################
add_executable (${PROJECT_NAME} 
	"src/main.cpp"
	"src/pch.cpp"
	"src/playVideoWithAudio.cpp"
)


target_include_directories( ${PROJECT_NAME}  
	PRIVATE 
		${PROJECT_SOURCE_DIR}/include
		${AVCODEC_INCLUDE_DIR} 
		${AVFORMAT_INCLUDE_DIR} 
		${AVUTIL_INCLUDE_DIR} 
		${AVDEVICE_INCLUDE_DIR}
		${AVFILTER_INCLUDE_DIR}
		${POSTPROC_INCLUDE_DIR}
		${SWRESAMPLE_INCLUDE_DIR}
		${SWSCALE_INCLUDE_DIR}
		${SDL_INCLUDE_DIR}
		${OpenAL_INCLUDE_DIR}
)

target_link_libraries( ${PROJECT_NAME}  
	PRIVATE 
		${AVCODEC_LIBRARY} 
		${AVFORMAT_LIBRARY} 
		${AVUTIL_LIBRARY} 
		${AVDEVICE_LIBRARY}
		${AVFILTER_LIBRARY}
		${POSTPROC_LIBRARY}
		${SWRESAMPLE_LIBRARY}
		${SWSCALE_LIBRARY}
		${SDL_LIBRARY}
		${OpenAL_LIBRARY}

)


