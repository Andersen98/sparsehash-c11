#include_directories(.)
#cmake_policy(PUSH) 
#cmake_minimum_required(VERSION 3.20)


#project(sparshash_gtest_pkgconfig VERSION 0.0.1 LANGUAGES CXX)



include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG  main
  )
# For Windows: Prevent overriding the parent project's compiler/linker settings
#set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)


#add_executable( sparsetable_unittests  sparsetable_unittests.cc)
#add_executable( simple_unittests  simple_unittests.cc)
#add_executable(hashtable_unittests hashtable_unittests.cc)
#add_executable(hashtable_c11_unittests hashtable_c11_unittests.cc)
#add_executable(fixture_unittests fixture_unittests.cc)
#add_executable( allocator_unittests  allocator_unittests.cc)
#add_executable( dense_hash_set_unittests dense_hash_set_unittests.cc)
#add_executable( dense_hash_map_unittests  dense_hash_map_unittests.cc)

enable_testing()

add_executable( sparshash_tests 
#  sparsetable_unittests.cc
  simple_unittests.cc
 # hashtable_unittests.cc
 # hashtable_c11_unittests.cc
 # fixture_unittests.cc
  #allocator_unittests.cc
  dense_hash_set_unittests.cc
  dense_hash_map_unittests.cc
  )



target_link_libraries(sparshash_tests ${GTEST_LDFLAGS} google_sparsehash)
target_compile_options(sparshash_tests  PUBLIC ${GTEST_CFLAGS})  

include(GoogleTest)
gtest_discover_tests( sparshash_tests 
  DISCOVERY_MODE PRE_TEST
  )
