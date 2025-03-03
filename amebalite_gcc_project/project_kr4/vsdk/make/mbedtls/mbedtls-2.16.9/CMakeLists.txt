set(DIR ${BASEDIR}/component/ssl/mbedtls-${MBEDTLS_VER})
set(MODULE_C_DEFINES CONFIG_BUILD_NONSECURE=1)
set(MODULE_C_OPTIONS -Wno-unused-const-variable)

set(CSRC)

if(NOT CONFIG_MP_INCLUDED)
    if(CONFIG_WLAN)
        if(CONFIG_AS_INIC_AP OR CONFIG_SINGLE_CORE_WIFI)
            list(
                APPEND CSRC
                ${DIR}/library/net_sockets.c
            )
        endif()
    endif()
endif()

list(
    APPEND CSRC
    ${DIR}/library/aes.c
    ${DIR}/library/aesni.c
    ${DIR}/library/blowfish.c
    ${DIR}/library/camellia.c
    ${DIR}/library/ccm.c
    ${DIR}/library/certs.c
    ${DIR}/library/cipher.c
    ${DIR}/library/cipher_wrap.c
    ${DIR}/library/cmac.c
    ${DIR}/library/debug.c
    ${DIR}/library/error.c
    ${DIR}/library/entropy.c
    ${DIR}/library/gcm.c
    ${DIR}/library/havege.c
    ${DIR}/library/memory_buffer_alloc.c
    ${DIR}/library/padlock.c
    ${DIR}/library/pkcs5.c
    ${DIR}/library/pkcs11.c
    ${DIR}/library/pkcs12.c
    ${DIR}/library/pkparse.c
    ${DIR}/library/platform.c
    ${DIR}/library/ssl_cache.c
    ${DIR}/library/ssl_cli.c
    ${DIR}/library/ssl_srv.c
    ${DIR}/library/ssl_ciphersuites.c
    ${DIR}/library/ssl_ticket.c
    ${DIR}/library/ssl_tls.c
    ${DIR}/library/threading.c
    ${DIR}/library/timing.c
    ${DIR}/library/version.c
    ${DIR}/library/version_features.c
    ${DIR}/library/x509.c
    ${DIR}/library/x509_create.c
    ${DIR}/library/x509_crl.c
    ${DIR}/library/x509_crt.c
    ${DIR}/library/x509_csr.c
    ${DIR}/library/x509write_crt.c
    ${DIR}/library/x509write_csr.c
    ${DIR}/library/rsa.c
    ${DIR}/library/arc4.c
    ${DIR}/library/ctr_drbg.c
    ${DIR}/library/rsa_internal.c
    ${DIR}/library/ctr_drbg.c
)

if(CONFIG_RLE1080_A_CUT)
    list(APPEND CSRC ${DIR}/library/platform_util.c)
endif()

list(
    APPEND CSRC
    ${DIR}/library/dhm.c
	${DIR}/library/hmac_drbg.c
	${DIR}/library/pem.c
	${DIR}/library/pk.c
	${DIR}/library/pk_wrap.c
	${DIR}/library/pkwrite.c
	${DIR}/library/rsa.c
	${DIR}/library/oid.c
	${DIR}/library/base64.c
	#${DIR}/library/ecdh.c	\
	#${DIR}/library/ecdsa.c	\
)


ameba_internal_library(mbedtls)
target_compile_definitions(${CURRENT_LIB_NAME} PRIVATE ${MODULE_C_DEFINES})
target_compile_options(${CURRENT_LIB_NAME} PRIVATE ${MODULE_C_OPTIONS})
target_sources(${CURRENT_LIB_NAME} PRIVATE ${CSRC})
