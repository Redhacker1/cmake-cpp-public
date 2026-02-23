cmake_minimum_required( VERSION 3.16 )

project( jpeglib C )

#set( CMAKE_CXX_STANDARD 11 )

add_library(libjpeg STATIC)

target_include_directories(libjpeg PUBLIC ${CMAKE_CURRENT_LIST_DIR})

target_sources(libjpeg PUBLIC
        cdjpeg.c
        jcapistd.c
        jcapimin.c
        jccoefct.c
        jccolor.c
        jcdctmgr.c
        jchuff.c
        jcinit.c
        jcmainct.c
        jcmarker.c
        jcmaster.c
        jcomapi.c
        jcparam.c
        jcphuff.c
        jcprepct.c
        jcsample.c
        jctrans.c

        jdapimin.c
        jdapistd.c
        jdatadst.c
        jdatasrc.c
        jdcoefct.c
        jdcolor.c
        jddctmgr.c
        jdhuff.c
        jdinput.c
        jdmainct.c
        jdmarker.c
        jdmaster.c
        jdmerge.c
        jdphuff.c
        jdpostct.c
        jdsample.c
        jdtrans.c

        jerror.c
        jutils.c
        jmemmgr.c
        jmemnobs.c

        jfdctflt.c
        jfdctfst.c
        jfdctint.c
        jidctflt.c
        jidctfst.c
        jidctint.c
        jidctred.c
        jquant1.c
        jquant2.c
)