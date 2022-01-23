cmake_minimum_required(VERSION 3.20)



set(CMAKE_BUILD_TYPE Release)
project (google_sparsehash
  VERSION 2.11.1
  LANGUAGES CXX
  )  



add_library(google_sparsehash INTERFACE
  src/sparsehash/dense_hash_map
  src/sparsehash/dense_hash_set
  src/sparsehash/sparse_hash_map
  src/sparsehash/sparse_hash_set
  src/sparsehash/sparsetable
  src/sparsehash/traits
  src/sparsehash/internal/densehashtable.h
  src/sparsehash/internal/hashtable-common.h
  src/sparsehash/internal/libc_allocator_with_realloc.h
  src/sparsehash/internal/sparsehashtable.h
  )


target_include_directories(google_sparsehash INTERFACE
  # Ok, relocatable:
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>"
  "$<INSTALL_INTERFACE:$<INSTALL_PREFIX>include/google>"
  )


  

add_executable(bench bench.cc)
target_link_libraries(bench google_sparsehash)

add_subdirectory(tests)
include(GNUInstallDirs)

install( DIRECTORY src/ TYPE INCLUDE )

#credit to CLIUtils/modern-cmake for this code 
# Testing only available if this is the main app
# Emergency override SPARSEHASH_CMAKE_BUILD_TESTING provided as well
if((CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME OR SPARSHASH_CMAKE_BUILD_TESTING)
    AND BUILD_TESTING)
  add_subdirectory(tests)
endif()
