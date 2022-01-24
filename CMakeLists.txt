cmake_minimum_required(VERSION 3.17.2)
project (GoogleSparseHash)



# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
include(GNUInstallDirs)

add_library(GoogleSparseHash INTERFACE)
target_include_directories(GoogleSparseHash INTERFACE
  # Ok, relocatable:
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src/sparshash>"
  )

install(TARGETS GoogleSparseHash EXPORT googlesparsehashExport)
install(EXPORT googlesparsehashExport NAMESPACE Upstream::
  DESTINATION lib/cmake/GoogleSparseHash
  )
  
  


install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/dense_hash_map
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/dense_hash_set
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/sparse_hash_map
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/sparse_hash_set
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/sparsetable
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/traits
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/sparsehash 
  )

install(FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/internal/densehashtable.h
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/internal/hashtable-common.h
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/internal/libc_allocator_with_realloc.h
  ${CMAKE_CURRENT_SOURCE_DIR}/src/sparsehash/internal/sparsehashtable.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/sparsehash/internal
  )

if(BUILD_TESTING)
add_subdirectory(tests)
target_include_directories(sparshash_tests PRIVATE  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>)
endif()

add_executable(bench bench.cc)
target_link_libraries(bench PRIVATE GoogleSparseHash)
target_include_directories(bench PRIVATE  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>)
