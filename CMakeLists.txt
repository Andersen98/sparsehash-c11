cmake_minimum_required(VERSION 3.17.2)
project (Google_Sparsehash
  VERSION 2.11.1
  LANGUAGES CXX
  )  


# GoogleTest requires at least C++11
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_BUILD_TYPE Release)

include(GNUInstallDirs)



#add_library(google_sparsehash INTERFACE
  

#target_include_directories(google_sparsehash INTERFACE
  # Ok, relocatable:
 # "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>"
 # "$<INSTALL_INTERFACE:$<INSTALL_PREFIX>include/google>"
 # )




#add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/tests")  


#add_executable(bench bench.cc)
#target_link_libraries(bench PRIVATE google_sparsehash)

set(HEADERS_INTERNAL
  src/sparsehash/internal/densehashtable.h
  src/sparsehash/internal/hashtable-common.h
  src/sparsehash/internal/libc_allocator_with_realloc.h
  src/sparsehash/internal/sparsehashtable.h
  )
  

set(HEADERS_BASE
  src/sparsehash/dense_hash_map
  src/sparsehash/dense_hash_set
  src/sparsehash/sparse_hash_map
  src/sparsehash/sparse_hash_set
  src/sparsehash/sparsetable
  src/sparsehash/traits
  src/sparsehash/dense_hash_map
  src/sparsehash/dense_hash_set
  src/sparsehash/sparse_hash_map
  src/sparsehash/sparse_hash_set
  src/sparsehash/sparsetable
  src/sparsehash/traits
)

install(FILES ${HEADERS_BASE} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/sparsehash)
install(FILES ${HEADERS_INTERNAL} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/sparsehash/internal)
