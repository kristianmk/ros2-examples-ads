# Written by Kristian Muri Knausgård 2022-03-28
#
cmake_minimum_required(VERSION 3.8)
project(ads_example)


# Posix threads
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

# ADS library from Beckhoff (assumed pre-built, follow the instructions in git submodule ADS).
find_library(
    LIBADS_LIBRARY
    NAMES AdsLib
    HINTS "../ADS/build"
)

# Source file (Beckhoff example).
set(SOURCES
  ads_example.cpp
)

add_executable(ads_example ${SOURCES})

target_link_libraries(ads_example PUBLIC ${LIBADS_LIBRARY} Threads::Threads)
target_include_directories(ads_example PRIVATE "../ADS/AdsLib")
