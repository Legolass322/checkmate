# minimum 3.1 for CMAKE_CXX_STANDARD_REQUIRED
cmake_minimum_required(VERSION 3.11)
project(checkmate)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
include(FetchContent)

FetchContent_Declare(z3
	GIT_REPOSITORY https://github.com/Z3Prover/z3
	GIT_TAG        z3-4.12.1
)
FetchContent_MakeAvailable(z3)

include_directories( ${z3_SOURCE_DIR}/src/api )

add_executable(checkmate
	src/json.hpp
	src/input.hpp
	src/input.cpp
	src/options.hpp
	src/options.cpp
	src/property.hpp
	src/property.cpp
	src/utility.hpp
	src/utils.hpp
	src/z3++.hpp
	src/z3++.cpp
	src/checkmate.cpp
)
target_link_libraries(checkmate z3 libz3)

# add extra warnings for GCC/Clang
if(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
	target_compile_options(checkmate PRIVATE -Wall -Wextra -Wpedantic)
endif()
