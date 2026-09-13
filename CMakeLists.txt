cmake_minimum_required(VERSION 3.16)

if (DEFINED ESP_PLATFORM)
  # idf component
  # encode.c/decode.c are standalone CLI test tools with their own main() - excluded from the library
  file(GLOB G7XX_SRCS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
  list(REMOVE_ITEM G7XX_SRCS "${CMAKE_CURRENT_SOURCE_DIR}/src/encode.c" "${CMAKE_CURRENT_SOURCE_DIR}/src/decode.c")

  idf_component_register(
      SRCS ${G7XX_SRCS}
      INCLUDE_DIRS src
  )

  target_compile_options(${COMPONENT_LIB} PUBLIC -Wno-error)

else()

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

endif()
