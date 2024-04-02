# Written by Kristian Muri Knausgård, last update 2024-04-02
#
cmake_minimum_required(VERSION 3.8)
project(ads_example)


# ADS library from Beckhoff
include(FetchContent)

FetchContent_Declare(
  ads
  GIT_REPOSITORY https://github.com/Beckhoff/ADS.git
  GIT_TAG        46873c1  # v20
)

FetchContent_GetProperties(ads)
if(NOT ads_POPULATED)
  FetchContent_Populate(ads)
  # Assuming Meson and Ninja are available in the system path!
  execute_process(
    COMMAND meson setup ${ads_SOURCE_DIR} ${ads_BINARY_DIR} -Ddefault_library=static
    WORKING_DIRECTORY ${ads_SOURCE_DIR}
  )
  execute_process(
    COMMAND ninja -C ${ads_BINARY_DIR}
    WORKING_DIRECTORY ${ads_SOURCE_DIR}
  )
endif()



# Posix threads
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)


# Source file (Beckhoff example).
set(SOURCES
  ads_example.cpp
)

add_executable(ads_example ${SOURCES})


target_link_libraries(ads_example PUBLIC ${ads_BINARY_DIR}/libAdsLib.a Threads::Threads)
target_include_directories(ads_example PRIVATE ${ads_SOURCE_DIR}/AdsLib)
