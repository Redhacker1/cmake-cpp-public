cmake_minimum_required( VERSION 3.16 )

project( curl C )

add_library(libcurl STATIC)

target_include_directories(libcurl PUBLIC include)
target_include_directories(libcurl PRIVATE lib)

target_compile_definitions(libcurl PUBLIC CURL_STATICLIB)
target_compile_definitions(libcurl PRIVATE BUILDING_LIBCURL)

if(UNIX AND NOT APPLE)
    # For generic Unix (like Linux), we might need some basic definitions
    # if we don't have a hand-crafted config-linux.h
    target_compile_definitions(libcurl PRIVATE 
        HAVE_CONFIG_H
        HAVE_STDLIB_H HAVE_STRING_H HAVE_STRDUP HAVE_SOCKET HAVE_SELECT 
        HAVE_NETINET_IN_H HAVE_NETDB_H HAVE_ARPA_INET_H HAVE_UNISTD_H 
        HAVE_FCNTL_H HAVE_SYS_STAT_H HAVE_SYS_TYPES_H HAVE_TIME_H
        HAVE_GETTIMEOFDAY HAVE_SIGACTION HAVE_SIGNAL_H
        HAVE_RECV HAVE_SEND HAVE_RECVFROM
    )
endif()

target_sources(libcurl PRIVATE
        lib/amigaos.c
        lib/base64.c
        lib/connect.c
        lib/content_encoding.c
        lib/cookie.c
        lib/curl_addrinfo.c
        lib/curl_fnmatch.c
        lib/curl_gethostname.c
        lib/curl_memrchr.c
        lib/curl_rand.c
        lib/curl_rtmp.c
        lib/curl_sspi.c
        lib/curl_threads.c
        lib/dict.c
        lib/easy.c
        lib/escape.c
        lib/file.c
        lib/fileinfo.c
        lib/formdata.c
        lib/ftp.c
        lib/ftplistparser.c
        lib/getenv.c
        lib/getinfo.c
        lib/gtls.c
        lib/hash.c
        lib/hmac.c
        lib/hostares.c
        lib/hostasyn.c
        lib/hostip.c
        lib/hostip4.c
        lib/hostip6.c
        lib/hostsyn.c
        lib/hostthre.c
        lib/http.c
        lib/http_chunks.c
        lib/http_digest.c
        lib/http_negotiate.c
        lib/http_ntlm.c
        lib/if2ip.c
        lib/imap.c
        lib/inet_ntop.c
        lib/inet_pton.c
        lib/krb4.c
        lib/krb5.c
        lib/ldap.c
        lib/llist.c
        lib/md4.c
        lib/md5.c
        lib/memdebug.c
        lib/mprintf.c
        lib/multi.c
        lib/netrc.c
        lib/nonblock.c
        lib/nss.c
        lib/nwlib.c
        lib/nwos.c
        lib/openldap.c
        lib/parsedate.c
        lib/pingpong.c
        lib/polarssl.c
        lib/pop3.c
        lib/progress.c
        lib/qssl.c
        lib/rawstr.c
        lib/rtsp.c
        lib/security.c
        lib/select.c
        lib/sendf.c
        lib/share.c
        lib/slist.c
        lib/smtp.c
        lib/socks.c
        lib/socks_gssapi.c
        lib/socks_sspi.c
        lib/speedcheck.c
        lib/splay.c
        lib/ssh.c
        lib/sslgen.c
        lib/ssluse.c
        lib/strdup.c
        lib/strequal.c
        lib/strerror.c
        lib/strtok.c
        lib/strtoofft.c
        lib/telnet.c
        lib/tftp.c
        lib/timeval.c
        lib/transfer.c
        lib/url.c
        lib/version.c
        lib/warnless.c
        lib/wildcard.c
)

if(WIN32)
    target_link_libraries(libcurl PUBLIC ws2_32 winmm wsock32 crypt32)
elseif(APPLE)
    target_link_libraries(libcurl PUBLIC "-framework CoreFoundation" "-framework SystemConfiguration")
elseif(UNIX)
    target_link_libraries(libcurl PUBLIC pthread rt m resolv dl)
endif()