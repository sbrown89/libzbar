cmake_minimum_required(VERSION 3.3)

add_subdirectory("decoder")
add_subdirectory("qrcode")

set(SOURCES
    config.c
    decoder.c
    error.c
    image.c
    img_scanner.c
    refcnt.c
    scanner.c
    symbol.c
)

set(HEADERS
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

add_library(${LZBAR} SHARED ${SOURCES} ${HEADERS})
add_library("${LZBAR}-static" STATIC ${SOURCES} ${HEADERS})

target_link_libraries(${LZBAR} ${LQRCODE} ${LDECODER})
target_link_libraries("${LZBAR}-static" ${LQRCODE} ${LDECODER})

install(TARGETS ${LZBAR} DESTINATION ${CMAKE_INSTALL_PREFIX})
install(TARGETS "${LZBAR}-static" DESTINATION ${CMAKE_INSTALL_PREFIX})
