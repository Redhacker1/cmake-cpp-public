cmake_minimum_required( VERSION 3.16 )

project( libpng C )

#add_subdirectory("../zlib" "zlib_build")

#set( CMAKE_CXX_STANDARD 11 )

add_library(libpnglib STATIC)

target_include_directories(libpnglib PUBLIC ${CMAKE_CURRENT_LIST_DIR})

target_sources(libpnglib PRIVATE
        png.c
        pngerror.c
        pnggccrd.c
        pngget.c
        pngmem.c
        pngpread.c
        pngread.c
        pngrio.c
        pngrtran.c
        pngrutil.c
        pngset.c
        pngtrans.c
        #pngvcrd.c
        pngwio.c
        pngwrite.c
        pngwtran.c
        pngwutil.c
)

target_link_libraries(libpnglib PUBLIC zlib)