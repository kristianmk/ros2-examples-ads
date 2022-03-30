cmake_minimum_required(VERSION 3.8)
project(ads_example_package)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

# Posix threads
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

# ADS library from Beckhoff (assumed pre-built, follow the instructions in git submodule ADS).
find_library(
    LIBADS_LIBRARY
    NAMES AdsLib
    HINTS "../ADS/build"
)



add_executable(ads_node src/ads_node.cpp)


target_compile_features(ads_node PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17

target_include_directories(ads_node PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
target_include_directories(ads_node PRIVATE "../ADS/AdsLib")

target_link_libraries(ads_node PUBLIC ${LIBADS_LIBRARY} Threads::Threads)


install(TARGETS ads_node
  DESTINATION lib/${PROJECT_NAME})



if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
