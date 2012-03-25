cmake_minimum_required(VERSION 2.8)

project(cloudfuse)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

find_package(libxml2 REQUIRED)
include_directories(${LIBXML2_INCLUDE_DIR})

find_package(CURL REQUIRED)
include_directories(${CURL_INCLUDE_DIRS})

find_package(OpenSSL REQUIRED)
include_directories(${OPENSSL_INCLUDE_DIR})

include_directories("/usr/local/include/osxfuse") # OSXFuse for Mac
add_definitions(-D_FILE_OFFSET_BITS=64) # OSXFuse told me to do it :)

add_executable(cloudfuse cloudfuse.c cloudfsapi.c)
target_link_libraries(cloudfuse fuse ${LIBXML2_LIBRARIES} ${CURL_LIBRARIES} ${OPENSSL_LIBRARIES})
