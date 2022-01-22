cmake_minimum_required(VERSION 3.20)



set(CMAKE_BUILD_TYPE Release)
project (google_sparsehash
  VERSION 2.11.1
  LANGUAGES CXX
  )

#only do this if we are the main project
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
  

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")



add_subdirectory(src)
add_subdirectory(tests)

#credit to CLIUtils/modern-cmake for this code 
# Testing only available if this is the main app
# Emergency override SPARSEHASH_CMAKE_BUILD_TESTING provided as well
if((CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME OR SPARSHASH_CMAKE_BUILD_TESTING)
    AND BUILD_TESTING)
  add_subdirectory(tests)
endif()
