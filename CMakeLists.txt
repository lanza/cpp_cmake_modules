cmake_minimum_required(VERSION 3.26)

set(CMAKE_EXPERIMENTAL_CXX_MODULE_CMAKE_API "2182bf5c-ef0d-489a-91da-49dbc3090d2a")
set(CMake_TEST_MODULE_COMPILATION named,shared,partitions,internal_partitions,export_bmi,install_bmi)
set(CMake_TEST_MODULE_COMPILATION_RULES /Users/lanza/Projects/cmake/source/tree/.gitlab/ci/cxx_modules_rules_clang.cmake)

set(CMAKE_EXPERIMENTAL_CXX_MODULE_DYNDEP 1)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 20)

set(CLANG_ROOT $ENV{HOME}/.llvm)
set(CMAKE_CXX_COMPILER ${CLANG_ROOT}/bin/clang++)
set(CMAKE_C_COMPILER ${CLANG_ROOT}/bin/clang)

project(test C CXX)

add_library(foo)
target_sources(foo
  PUBLIC
  FILE_SET cxx_modules
    BASE_DIRS
      ${CMAKE_CURRENT_SOURCE_DIR}
    TYPE
      CXX_MODULES
    FILES
      foo.cpp
)

add_executable(main)
target_link_libraries(main foo)
target_sources(main
  PRIVATE
    main.cpp)
