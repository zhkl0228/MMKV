# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_FLAGS "-std=c++11 -fno-exceptions -fvisibility=hidden -fno-unwind-tables -fno-asynchronous-unwind-tables")
set(CMAKE_SHARED_LINKER_FLAGS "-static-libgcc -static-libstdc++")

find_package(JNI REQUIRED)
include_directories(${JAVA_INCLUDE_PATH})
include_directories(${JAVA_INCLUDE_PATH2})

if (NOT EXISTS ${CMAKE_BINARY_DIR}/CMakeCache.txt)
  if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)
  endif()
endif()

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             mmkv

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/native-bridge.cpp
             src/main/cpp/MMKV.h
             src/main/cpp/MMKV.cpp
             src/main/cpp/MMKVLog.h
             src/main/cpp/MMKVLog.cpp
             src/main/cpp/CodedInputData.h
             src/main/cpp/CodedInputData.cpp
             src/main/cpp/CodedOutputData.h
             src/main/cpp/CodedOutputData.cpp
             src/main/cpp/PBUtility.h
             src/main/cpp/PBUtility.cpp
             src/main/cpp/MiniPBCoder.h
             src/main/cpp/MiniPBCoder.cpp
             src/main/cpp/MMBuffer.h
             src/main/cpp/MMBuffer.cpp
             src/main/cpp/InterProcessLock.h
             src/main/cpp/InterProcessLock.cpp
             src/main/cpp/MmapedFile.h
             src/main/cpp/MmapedFile.cpp
             src/main/cpp/ThreadLock.h
             src/main/cpp/ThreadLock.cpp
             src/main/cpp/MMKVMetaInfo.hpp
             src/main/cpp/aes/AESCrypt.h
             src/main/cpp/aes/AESCrypt.cpp
             src/main/cpp/aes/openssl/aes.h
             src/main/cpp/aes/openssl/aes_cfb.c
             src/main/cpp/aes/openssl/aes_core.c
             src/main/cpp/aes/openssl/aes_locl.h
             src/main/cpp/aes/openssl/cfb128.c
             src/main/cpp/aes/openssl/modes.h
             src/main/cpp/aes/openssl/opensslconf.h
             src/main/cpp/aes/openssl/md5_dgst.c
             src/main/cpp/aes/openssl/md5_locl.h
             src/main/cpp/aes/openssl/md5_one.c
             src/main/cpp/aes/openssl/md5.h
             src/main/cpp/aes/openssl/md32_common.h
             )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       mmkv

                       # Links the target library to the log library
                       # included in the NDK.
                       z )
