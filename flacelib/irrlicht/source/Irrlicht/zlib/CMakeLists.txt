cmake_minimum_required( VERSION 3.16 )

project( libzlib C )

#set( CMAKE_CXX_STANDARD 11 )

add_library(zlib STATIC)

target_include_directories(zlib PUBLIC ${CMAKE_CURRENT_LIST_DIR})

target_sources(zlib PRIVATE
        adler32.c
        compress.c
        crc32.c
        deflate.c
        gzclose.c
        gzlib.c
        gzread.c
        gzwrite.c
        infback.c
        inftrees.c
        inffast.c
        inflate.c
        trees.c
        uncompr.c
        zutil.c
)