cmake_minimum_required(VERSION 3.16)

# set the project name
project(arduino_libgxx)

# lots of warnings and all warnings as errors
## add_compile_options(-Wall -Wextra )
set(CMAKE_CXX_STANDARD 17)

file(GLOB_RECURSE SRC_LIST_C CONFIGURE_DEPENDS  "${PROJECT_SOURCE_DIR}/src/*.c" )

# define libraries
add_library (arduino_libgxx ${SRC_LIST_C})

target_compile_options(arduino_libgxx PRIVATE -Wdouble-promotion)
target_compile_definitions(arduino_libgxx PUBLIC -DARDUINO )


# define location for header files
target_include_directories(arduino_libgxx PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src )
