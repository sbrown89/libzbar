cmake_minimum_required(VERSION 3.3)
project("libzbar" VERSION 0.11.0 DESCRIPTION "Complete cross-platform ZBar cmake port")
if(NOT CMAKE_INSTALL_PREFIX)
    set(CMAKE_INSTALL_PREFIX "${PROJECT_SOURCE_DIR}/bin")
endif()

set(CMAKE_VERBOSE_MAKEFILE OFF)
set(CMAKE_CONFIGURATION_TYPES "Debug;Release")

if(WIN32)
    set(CMAKE_C_FLAGS_RELEASE "/O2 /TC")
    set(CMAKE_C_FLAGS_DEBUG "/Zi /TC")
elseif(UNIX)
    set(CMAKE_C_FLAGS_RELEASE "-O3 -fPIC")
    set(CMAKE_C_FLAGS_DEBUG "-Og -fPIC")
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS_RELEASE}")
elseif(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS_DEBUG}")
endif()

include_directories("${PROJECT_SOURCE_DIR}/include")
include_directories("${PROJECT_SOURCE_DIR}/zbar/decoder")
include_directories("${PROJECT_SOURCE_DIR}/zbar/qrcode")
include_directories("${PROJECT_SOURCE_DIR}/zbar")
set(ZBAR_MAIN   "${PROJECT_SOURCE_DIR}/include/zbar.h")

set(LIOCONV     "lioconv-win")
set(LCONFIG     "lconfig")
set(LDECODER    "ldecoder")
set(LQRCODE     "lqrcode")
set(LZBAR       "libzbar")

if(WIN32)
    include_directories("${PROJECT_SOURCE_DIR}/zbar/libiconv-win/include")
endif(WIN32)

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
