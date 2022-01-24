project(GoogleSparseHashTests)
include(GNUInstallDirs)
add_executable( sparshash_tests
  sparsetable_unittests.cc
  simple_unittests.cc
  hashtable_unittests.cc
  hashtable_c11_unittests.cc
  fixture_unittests.cc
  allocator_unittests.cc
  dense_hash_set_unittests.cc
  dense_hash_map_unittests.cc
  )


include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG  main
  )
# For Windows: Prevent overriding the parent project's compiler/linker settings
#set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)


enable_testing()



target_link_libraries(sparshash_tests PRIVATE GoogleSparseHash  PRIVATE  gtest_main PRIVATE gmock_main  )

include(GoogleTest)
gtest_discover_tests( sparshash_tests
  DISCOVERY_MODE PRE_TEST
  )
