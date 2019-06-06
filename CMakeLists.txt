cmake_minimum_required(VERSION 3.3)
project("ZBar" VERSION 1.0.0 DESCRIPTION "ZBar cmake port")
set(CMAKE_INSTALL_PREFIX "${PROJECT_SOURCE_DIR}/bin")
set(CMAKE_VERBOSE_MAKEFILE OFF)
set(CMAKE_CONFIGURATION_TYPES "Debug;Release")
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -fPIC")
set(CMAKE_C_FLAGS_RELEASE "-O3 -fPIC")
set(CMAKE_CXX_FLAGS_DEBUG "-Og -fPIC")
set(CMAKE_C_FLAGS_DEBUG "-Og -fPIC")
set(CXX_VER "-std=c++11")

if(CMAKE_CXX_STANDARD EQUAL 11)
    set(CXX_VER "-std=c++11")
elseif(CMAKE_CXX_STANDARD EQUAL 14)
    set(CXX_VER "-std=c++14")
elseif(CMAKE_CXX_STANDARD EQUAL 17)
    set(CXX_VER "-std=c++17")
else()
    set(CXX_VER "-std=c++11")
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_CXX_FLAGS "${CXX_VER} ${CMAKE_CXX_FLAGS_RELEASE}")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS_RELEASE}")
elseif(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_CXX_FLAGS "${CXX_VER} ${CMAKE_CXX_FLAGS_DEBUG}")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS_DEBUG}")
endif()

include_directories("${PROJECT_SOURCE_DIR}/include")
include_directories("${PROJECT_SOURCE_DIR}/zbar/decoder")
include_directories("${PROJECT_SOURCE_DIR}/zbar/qrcode")
include_directories("${PROJECT_SOURCE_DIR}/zbar")

set(LCONFIG     "lconfig")
set(LDECODER    "ldecoder")
set(LQRCODE     "lqrcode")
set(LZBAR       "lzbar")

add_subdirectory("zbar")

set(PUBLIC_HEADERS
    "${PROJECT_SOURCE_DIR}/include/zbar.h"
)

set(NON_PUBLIC_HEADERS
    "${PROJECT_SOURCE_DIR}/include/zbar/zbargtk.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Symbol.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Exception.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Processor.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/QZBar.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/ImageScanner.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Decoder.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/QZBarImage.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Video.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Scanner.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Image.h"
    "${PROJECT_SOURCE_DIR}/include/zbar/Window.h"
)

install(FILES ${PUBLIC_HEADERS} DESTINATION "${CMAKE_INSTALL_PREFIX}/include")
install(FILES ${NON_PUBLIC_HEADERS} DESTINATION "${CMAKE_INSTALL_PREFIX}/include/zbar")

