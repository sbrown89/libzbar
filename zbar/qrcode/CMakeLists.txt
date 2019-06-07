cmake_minimum_required(VERSION 3.3)
set(SOURCES
    bch15_5.c
    binarize.c
    isaac.c
    qrdec.c
    qrdectxt.c
    rs.c
    util.c
)

set(HEADERS
    ${ZBAR_MAIN}
    bch15_5.h
    binarize.h
    isaac.h
    qrdec.h
    rs.h
    util.h
)

add_library(${LQRCODE} STATIC ${SOURCES} ${HEADERS})

if(UNIX)
    target_link_libraries(${LQRCODE} ${LCONFIG})
elseif(WIN32)
    target_link_libraries(${LQRCODE} ${LCONFIG} ${LIOCONV})
    target_compile_definitions(${LQRCODE} PUBLIC LIB_ZBAR_BUILD)
endif()
