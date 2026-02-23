cmake_minimum_required( VERSION 3.16 )

project( player CXX C )

set( CMAKE_CXX_STANDARD 20 )


add_executable(player WIN32)

target_sources(player PRIVATE
        win32player.cpp
        steamsupport.cpp
        registryHelper.cpp
        CPlayerScriptLib.cpp
        CPlayer.cpp
        COculusRiftSupport-0.3.cpp
        base64.cpp
)

target_link_libraries(player PRIVATE flacelib)