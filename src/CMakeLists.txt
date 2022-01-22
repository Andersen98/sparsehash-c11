include(CMakePackageConfigHelpers)


set(version 1.0.0)

set(google_sparsehash_headers
  sparsehash/dense_hash_map
  sparsehash/dense_hash_set
  sparsehash/sparse_hash_map
  sparsehash/sparse_hash_set
  sparsehash/sparsetable
  sparsehash/traits
  sparsehash/internal/densehashtable.h
  sparsehash/internal/hashtable-common.h
  sparsehash/internal/libc_allocator_with_realloc.h
  sparsehash/internal/sparsehashtable.h
  )
add_library(google_sparsehash INTERFACE ${google_sparsehash_headers})

target_include_directories(google_sparsehash INTERFACE
  # Ok, relocatable:
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/sparsehash>"
  "$<INSTALL_INTERFACE:$<INSTALL_PREFIX>/include/google>"
  )


set_property(TARGET google_sparsehash PROPERTY VERSION ${version})
set_property(TARGET google_sparsehash PROPERTY SOVERSION 1)
set_property(TARGET google_sparsehash PROPERTY
  INTERFACE_google_sparsehash_MAJOR_VERSION 1)
set_property(TARGET google_sparsehash APPEND PROPERTY
  COMPATIBLE_INTERFACE_STRING google_sparsehash_MAJOR_VERSION
  )

write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/google_sparsehashConfigVersion.cmake"
  VERSION "${version}"
  COMPATIBILITY AnyNewerVersion
  )

install(FILES ${google_sparsehash_headers}
  DESTINATION include/google
  )

