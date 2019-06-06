cmake_minimum_required(VERSION 3.3)

add_subdirectory("decoder")
add_subdirectory("qrcode")

set(SOURCES
    decoder.c
    error.c
    image.c
    img_scanner.c
    refcnt.c
    scanner.c
    symbol.c
)

set(HEADERS
    ${ZBAR_MAIN}
    debug.h
    decoder.h
    error.h
    image.h
    img_scanner.h
    qrcode.h
    refcnt.h
    svg.h
    symbol.h
)

set(SOURCES_CONFIG
    config.c
)

set(HEADERS_CONFIG
    config.h
)

add_library(${LCONFIG} STATIC ${SOURCES_CONFIG} ${HEADERS_CONFIG})
add_library(${LZBAR} SHARED ${SOURCES} ${HEADERS})
add_library("${LZBAR}-static" STATIC ${SOURCES} ${HEADERS})

set(C_HEADERS "")
set(CXX_HEADERS "")

if(UNIX)
    set(C_HEADERS "/usr/include")
    set(CXX_HEADERS "/usr/include/c++/${CMAKE_CXX_COMPILER_VERSION}")
endif(UNIX)

find_file(HAVE_DLFCN_F               "dlfcn.h" "${C_HEADERS}")
find_file(HAVE_FCNTL_F               "fcntl.h" "${C_HEADERS}")
find_file(HAVE_FEATURES_F            "features.h" "${C_HEADERS}")
find_file(HAVE_INTTYPES_F            "inttypes.h" "${C_HEADERS}")
find_file(HAVE_JPEGLIB_F             "jpeglib.h" "${C_HEADERS}")
find_file(HAVE_VIDEODEV2_F           "linux/videodev2.h" "${C_HEADERS}")
find_file(HAVE_VIDEODEV_F            "linux/videodev.h" "${C_HEADERS}")
find_file(HAVE_MEMORY_F              "memory.h" "${C_HEADERS}")
find_file(HAVE_POLL_F                "poll.h" "${C_HEADERS}")
find_file(HAVE_PTHREAD_F             "pthread.h" "${C_HEADERS}")
find_file(HAVE_STDINT_F              "stdint.h" "${C_HEADERS}")
find_file(HAVE_STDLIB_F              "stdlib.h" "${C_HEADERS}")
find_file(HAVE_STRINGS_F             "strings.h" "${C_HEADERS}")
find_file(HAVE_STRING_F              "string.h" "${C_HEADERS}")
find_file(HAVE_IOCTL_F               "sys/ioctl.h" "${C_HEADERS}")
find_file(HAVE_IPC_F                 "sys/ipc.h" "${C_HEADERS}")
find_file(HAVE_MMAN_F                "sys/mman.h" "${C_HEADERS}")
find_file(HAVE_SHM_F                 "sys/shm.h" "${C_HEADERS}")
find_file(HAVE_STAT_F                "sys/stat.h" "${C_HEADERS}")
find_file(HAVE_TIMES_F               "sys/times.h" "${C_HEADERS}")
find_file(HAVE_TIME_F                "sys/time.h" "${C_HEADERS}")
find_file(HAVE_TYPES_F               "sys/types.h" "${C_HEADERS}")
find_file(HAVE_UNISTD_F              "unistd.h" "${C_HEADERS}")
find_file(HAVE_VFW_F                 "vfw.h" "${C_HEADERS}")
find_file(HAVE_XSHM_F                "X11/extensions/XShm.h" "${C_HEADERS}")
find_file(HAVE_XVLIB_F               "X11/extensions/Xvlib.h" "${C_HEADERS}")

foreach(CONFIG_OPT
    ${HAVE_DLFCN_F}
    ${HAVE_FCNTL_F}
    ${HAVE_FEATURES_F}
    ${HAVE_INTTYPES_F}
    ${HAVE_JPEGLIB_F}
    ${HAVE_VIDEODEV2_F}
    ${HAVE_VIDEODEV_F}
    ${HAVE_MEMORY_F}
    ${HAVE_POLL_F}
    ${HAVE_PTHREAD_F}
    ${HAVE_STDINT_F}
    ${HAVE_STDLIB_F}
    ${HAVE_STRINGS_F}
    ${HAVE_STRING_F}
    ${HAVE_IOCTL_F}
    ${HAVE_IPC_F}
    ${HAVE_MMAN_F}
    ${HAVE_SHM_F}
    ${HAVE_STAT_F}
    ${HAVE_TIMES_F}
    ${HAVE_TIME_F}
    ${HAVE_TYPES_F}
    ${HAVE_UNISTD_F}
    ${HAVE_VFW_F}
    ${HAVE_XSHM_F}
    ${HAVE_XVLIB_F}
)
    if(EXISTS ${CONFIG_OPT})
        if(${CONFIG_OPT} STREQUAL ${HAVE_DLFCN_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_DLFCN)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_FCNTL_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_FCNTL)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_FEATURES_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_FEATURES)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_INTTYPES_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_INTTYPES)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_JPEGLIB_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_JPEGLIB)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_VIDEODEV2_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_VIDEODEV2)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_VIDEODEV_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_VIDEODEV)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_MEMORY_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_MEMORY)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_POLL_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_POLL)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_PTHREAD_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_PTHREAD)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_STDINT_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_STDINT)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_STDLIB_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_STDLIB)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_STRINGS_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_STRINGS)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_STRING_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_STRING)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_IOCTL_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_IOCTL)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_IPC_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_IPC)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_MMAN_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_MMAN)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_SHM_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_SHM)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_STAT_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_STAT)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_TIMES_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_TIMES)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_TIME_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_TIME)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_TYPES_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_TYPES)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_UNISTD_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_UNISTD)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_VFW_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_VFW)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_XSHM_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_XSHM)
        elseif(${CONFIG_OPT} STREQUAL ${HAVE_XVLIB_F})
            target_compile_definitions(${LCONFIG} PUBLIC HAVE_XVLIB)
        endif()
        
        message(STATUS "Found: ${CONFIG_OPT}")
    else()
        message(STATUS "Not-Found: ${CONFIG_OPT}")
    endif()
    
endforeach()

target_link_libraries(${LZBAR} ${LQRCODE} ${LDECODER} ${LCONFIG})
target_link_libraries("${LZBAR}-static" ${LQRCODE} ${LDECODER} ${LCONFIG})

install(TARGETS ${LZBAR} DESTINATION ${CMAKE_INSTALL_PREFIX})
