#include_directories(.)


include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG  main
  )
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)


set(sparsehash_unittests
    sparsetable_unittests.cc
    simple_unittests.cc
    hashtable_unittests.cc
    hashtable_c11_unittests.cc
    fixture_unittests.cc
    allocator_unittests.cc
    dense_hash_set_unittests.cc
    dense_hash_map_unittests.cc
    )

foreach(file sparsehash_unittests)
  cmake_path(GET "${file}" STEM fullstem)
  add_executable(fullstem file)
  target_link_libraries(fullstem gtest_main google_sparsehash)
  add_test(NAME "${fullstem}_test" COMMAND fullstem)
endforeach()
  

add_executable(bench bench.cc)


target_link_libraries(bench gtest_main google_sparsehash)
