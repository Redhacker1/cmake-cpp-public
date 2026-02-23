cmake_minimum_required( VERSION 3.10 )

project( irrklang CXX)
set( CMAKE_CXX_STANDARD 11 )

# 1. Architecture Detection
if( CMAKE_SIZEOF_VOID_P EQUAL 8 )
    set(ARCH_SUFFIX "_x64")
    set(ARCH_DIR "_64")
else()
    set(ARCH_SUFFIX "")
    set(ARCH_DIR "")
endif()

if(CMAKE_SYSTEM_PROCESSOR MATCHES "^(arm|aarch64)")
    message(FATAL_ERROR "ARM architecture detected. The irrklang binaries do not support ARM")
endif()

# 2. Platform Detection
if(WIN32 AND NOT MINGW)
    set(PLATFORM_SUFFIX "")
elseif (APPLE)
    set(PLATFORM_SUFFIX "macos_")
else()
    message( FATAL_ERROR "Unsupported platform for irrKlang: ${CMAKE_SYSTEM_NAME}")
endif ()

# 3. Build Type Detection
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(BUILD_SUFFIX "debug_")
    message(STATUS "Building irrKlang in Debug mode")

    if(APPLE)
        message(FATAL_ERROR "Debug builds of irrKlang are not available for macOS. Please switch to Release mode.")
    endif()
else()
    set(BUILD_SUFFIX "release_")
endif()

# 4. Import irrKlang
if(WIN32 AND NOT MINGW)
    if(CMAKE_BUILD_TYPE STREQUAL "Debug")
        # In Debug mode on Windows, we MUST use the dynamic library because only it has a Debug build.
        add_library(irrKlang SHARED IMPORTED GLOBAL)
        set_target_properties(irrKlang PROPERTIES
                IMPORTED_IMPLIB "${CMAKE_CURRENT_LIST_DIR}/debug_dynamic${ARCH_DIR}/irrKlang.lib"
                IMPORTED_LOCATION "${CMAKE_CURRENT_LIST_DIR}/debug_dynamic${ARCH_DIR}/irrKlang.dll"
                INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}/include"
        )
    else()
        # In Release mode on Windows, use the static library.
        add_library(irrKlang STATIC IMPORTED GLOBAL)
        set_target_properties(irrKlang PROPERTIES
                IMPORTED_LOCATION "${CMAKE_CURRENT_LIST_DIR}/release_static${ARCH_SUFFIX}/irrKlang.lib"
                INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}/include"
                INTERFACE_COMPILE_DEFINITIONS "IRRKLANG_STATIC"
        )
    endif()
elseif(APPLE)
    add_library(irrKlang STATIC IMPORTED GLOBAL)
    set_target_properties(irrKlang PROPERTIES
            IMPORTED_LOCATION "${CMAKE_CURRENT_LIST_DIR}/${PLATFORM_SUFFIX}${BUILD_SUFFIX}static/liblibirrklang.a"
            INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}/include"
            INTERFACE_COMPILE_DEFINITIONS "IRRKLANG_STATIC"
    )
endif()

# 5. Import irrKlang (Dynamic/Shared alias for backward compatibility or explicit use)
if(WIN32 AND NOT MINGW)
    if (NOT TARGET irrKlang_shared)
        add_library(irrKlang_shared SHARED IMPORTED GLOBAL)
        set_target_properties(irrKlang_shared PROPERTIES
                IMPORTED_IMPLIB "${CMAKE_CURRENT_LIST_DIR}/${BUILD_SUFFIX}dynamic${ARCH_DIR}/irrKlang.lib"
                IMPORTED_LOCATION "${CMAKE_CURRENT_LIST_DIR}/${BUILD_SUFFIX}dynamic${ARCH_DIR}/irrKlang.dll"
                INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}/include"
        )
    endif()
endif()

# 5.1 Copy DLL to binary directory
if(WIN32 AND NOT MINGW)
    if(CMAKE_BUILD_TYPE STREQUAL "Debug")
        set(DLL_SOURCE "${CMAKE_CURRENT_LIST_DIR}/debug_dynamic${ARCH_DIR}/irrKlang.dll")
    else()
        set(DLL_SOURCE "${CMAKE_CURRENT_LIST_DIR}/release_dynamic${ARCH_DIR}/irrKlang.dll")
    endif()

    if(EXISTS "${DLL_SOURCE}")
        # Copy to common binary directories where executables might be located
        file(COPY "${DLL_SOURCE}" DESTINATION "${CMAKE_BINARY_DIR}")
        file(COPY "${DLL_SOURCE}" DESTINATION "${CMAKE_BINARY_DIR}/win32player")
        message(STATUS "irrKlang DLL copied from ${DLL_SOURCE} to binary directories")
    endif()
endif()

# 6. Build ikpMP3 plugin from source
set(ikpMP3_SRCS
    ikpmp3src/CIrrKlangAudioStreamLoaderMP3.cpp
    ikpmp3src/CIrrKlangAudioStreamMP3.cpp
    ikpmp3src/ikpMP3.cpp
    ikpmp3src/decoder/bits.c
    ikpmp3src/decoder/mpaudec.c
)

add_library(ikpMP3 STATIC ${ikpMP3_SRCS})
target_include_directories(ikpMP3 PUBLIC
    "${CMAKE_CURRENT_LIST_DIR}/include"
)
target_include_directories(ikpMP3 PRIVATE
    "${CMAKE_CURRENT_LIST_DIR}/ikpmp3src"
    "${CMAKE_CURRENT_LIST_DIR}/ikpmp3src/decoder"
)
target_link_libraries(ikpMP3 PUBLIC irrKlang)



