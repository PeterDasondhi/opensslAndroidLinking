cmake_minimum_required(VERSION 3.4.1)

#
#set(distribution_DIR /home/leometric/Desktop/test/ndk-samples-master/hello-jni/distribution)
add_library(hello-jni SHARED
        hello-jni.c)

find_library (log-lib log)
#add the open ssl crypto lib
add_library(libcrypto STATIC IMPORTED)
set_target_properties(libcrypto PROPERTIES IMPORTED_LOCATION
        ${MY_OPENSSL_DIR}/${ANDROID_ABI}/lib/libcrypto.a)

# add the open ssl ssl lib

add_library(libssl STATIC IMPORTED)

set_target_properties(libssl PROPERTIES IMPORTED_LOCATION
        ${MY_OPENSSL_DIR}/${ANDROID_ABI}/lib/libssl.a)

#add to target_include_directories

target_include_directories(hello-jni PRIVATE  ${MY_OPENSSL_DIR}/include)


# Include libraries needed for hello-jni lib
target_link_libraries(hello-jni
        libssl
        libcrypto
        ${log-lib})
