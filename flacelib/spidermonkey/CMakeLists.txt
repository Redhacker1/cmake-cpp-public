cmake_minimum_required( VERSION 3.16 )

project( spidermonkey_js C )

#set( CMAKE_CXX_STANDARD 11 )

# Generate jsautokw.h
add_executable(jskwgen js/js/src/jskwgen.c)
target_include_directories(jskwgen PRIVATE js/js/src)
if(WIN32)
    target_compile_definitions(jskwgen PRIVATE XP_WIN _CRT_SECURE_NO_WARNINGS)
endif()

add_custom_command(
        OUTPUT "${CMAKE_CURRENT_SOURCE_DIR}/js/js/src/jsautokw.h"
        COMMAND jskwgen "${CMAKE_CURRENT_SOURCE_DIR}/js/js/src/jsautokw.h"
        DEPENDS jskwgen js/js/src/jskeyword.tbl
        WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/js/js/src"
        COMMENT "Generating jsautokw.h"
        VERBATIM
)

add_library(spidermonkey STATIC)

target_include_directories(spidermonkey PUBLIC
        js/js/src
        js/js/src/fdlibm
)

target_sources(spidermonkey PRIVATE
        js/js/src/jsautokw.h

        js/js/src/fdlibm/e_acos.c
        js/js/src/fdlibm/e_acosh.c
        js/js/src/fdlibm/e_asin.c
        js/js/src/fdlibm/e_atan2.c
        js/js/src/fdlibm/e_atanh.c
        js/js/src/fdlibm/e_cosh.c
        js/js/src/fdlibm/e_exp.c
        js/js/src/fdlibm/e_fmod.c
        js/js/src/fdlibm/e_gamma.c
        js/js/src/fdlibm/e_gamma_r.c
        js/js/src/fdlibm/e_hypot.c
        js/js/src/fdlibm/e_j0.c
        js/js/src/fdlibm/e_j1.c
        js/js/src/fdlibm/e_jn.c
        js/js/src/fdlibm/e_lgamma.c
        js/js/src/fdlibm/e_lgamma_r.c
        js/js/src/fdlibm/e_log.c
        js/js/src/fdlibm/e_log10.c
        js/js/src/fdlibm/e_pow.c
        js/js/src/fdlibm/e_rem_pio2.c
        js/js/src/fdlibm/e_remainder.c
        js/js/src/fdlibm/e_scalb.c
        js/js/src/fdlibm/e_sinh.c
        js/js/src/fdlibm/e_sqrt.c
        js/js/src/fdlibm/fdlibm.h
        js/js/src/fdlibm/fdlibm.mak
        js/js/src/fdlibm/fdlibm.mdp
        js/js/src/fdlibm/fdlibm.vcproj
        js/js/src/fdlibm/fdlibm-08.vcproj
        js/js/src/fdlibm/k_cos.c
        js/js/src/fdlibm/k_rem_pio2.c
        js/js/src/fdlibm/k_sin.c
        js/js/src/fdlibm/k_standard.c
        js/js/src/fdlibm/k_tan.c
        js/js/src/fdlibm/Makefile.in
        js/js/src/fdlibm/Makefile.ref
        js/js/src/fdlibm/s_asinh.c
        js/js/src/fdlibm/s_atan.c
        js/js/src/fdlibm/s_cbrt.c
        js/js/src/fdlibm/s_ceil.c
        js/js/src/fdlibm/s_copysign.c
        js/js/src/fdlibm/s_cos.c
        js/js/src/fdlibm/s_erf.c
        js/js/src/fdlibm/s_expm1.c
        js/js/src/fdlibm/s_fabs.c
        js/js/src/fdlibm/s_finite.c
        js/js/src/fdlibm/s_floor.c
        js/js/src/fdlibm/s_frexp.c
        js/js/src/fdlibm/s_ilogb.c
        js/js/src/fdlibm/s_isnan.c
        js/js/src/fdlibm/s_ldexp.c
        js/js/src/fdlibm/s_lib_version.c
        js/js/src/fdlibm/s_log1p.c
        js/js/src/fdlibm/s_logb.c
        js/js/src/fdlibm/s_matherr.c
        js/js/src/fdlibm/s_modf.c
        js/js/src/fdlibm/s_nextafter.c
        js/js/src/fdlibm/s_rint.c
        js/js/src/fdlibm/s_scalbn.c
        js/js/src/fdlibm/s_signgam.c
        js/js/src/fdlibm/s_significand.c
        js/js/src/fdlibm/s_sin.c
        js/js/src/fdlibm/s_tan.c
        js/js/src/fdlibm/s_tanh.c
        js/js/src/fdlibm/w_acos.c
        js/js/src/fdlibm/w_acosh.c
        js/js/src/fdlibm/w_asin.c
        js/js/src/fdlibm/w_atan2.c
        js/js/src/fdlibm/w_atanh.c
        js/js/src/fdlibm/w_cosh.c
        js/js/src/fdlibm/w_exp.c
        js/js/src/fdlibm/w_fmod.c
        js/js/src/fdlibm/w_gamma.c
        js/js/src/fdlibm/w_gamma_r.c
        js/js/src/fdlibm/w_hypot.c
        js/js/src/fdlibm/w_j0.c
        js/js/src/fdlibm/w_j1.c
        js/js/src/fdlibm/w_jn.c
        js/js/src/fdlibm/w_lgamma.c
        js/js/src/fdlibm/w_lgamma_r.c
        js/js/src/fdlibm/w_log.c
        js/js/src/fdlibm/w_log10.c
        js/js/src/fdlibm/w_pow.c
        js/js/src/fdlibm/w_remainder.c
        js/js/src/fdlibm/w_scalb.c
        js/js/src/fdlibm/w_sinh.c
        js/js/src/fdlibm/w_sqrt.c


        js/js/src/jsapi.c
        js/js/src/jsarena.c
        js/js/src/jsarray.c
        js/js/src/jsatom.c
        js/js/src/jsbool.c
        js/js/src/jscntxt.c
        js/js/src/jsconfig.h
        js/js/src/jsdate.c
        js/js/src/jsdbgapi.c
        js/js/src/jsdhash.c
        js/js/src/jsdtoa.c
        js/js/src/jsemit.c
        js/js/src/jsexn.c
        js/js/src/jsfun.c
        js/js/src/jsgc.c
        js/js/src/jshash.c
        js/js/src/jsinterp.c
        js/js/src/jsinvoke.c
        js/js/src/jsiter.c
        js/js/src/jslock.c
        js/js/src/jslog2.c
        js/js/src/jslong.c
        js/js/src/jsmath.c
        js/js/src/jsnum.c
        js/js/src/jsobj.c
        js/js/src/jsopcode.c
        js/js/src/jsparse.c
        js/js/src/jsprf.c
        js/js/src/jsregexp.c
        js/js/src/jsscan.c
        js/js/src/jsscope.c
        js/js/src/jsscript.c
        js/js/src/jsstddef.h
        js/js/src/jsstr.c
        js/js/src/jsutil.c
        js/js/src/jsxdrapi.c
        js/js/src/jsxml.c
        js/js/src/prmjtime.c
)

if(MINGW)
    target_link_libraries(spidermonkey winmm)
endif()

target_compile_definitions(spidermonkey PUBLIC STATIC_JS_API) # We build a static library always.

if (WIN32)
    target_compile_definitions(spidermonkey PUBLIC XP_WIN)
    target_compile_definitions(spidermonkey PRIVATE _CRT_SECURE_NO_WARNINGS)
    target_compile_definitions(spidermonkey PRIVATE _SCL_SECURE_NO_WARNINGS)
elseif (UNIX)
    target_compile_definitions(spidermonkey PUBLIC XP_UNIX)
endif ()


if( CMAKE_SIZEOF_VOID_P EQUAL 8 )
    target_compile_definitions(spidermonkey PRIVATE _M_X64)
else( CMAKE_SIZEOF_VOID_P EQUAL 4 )
    #set( BOOST_LIBRARY "/boost/win32/lib" )
endif()