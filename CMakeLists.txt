cmake_policy(SET CMP0048 NEW) # For using VERSION in "project"
project(akinopallete VERSION 1.0 DESCRIPTION "Pallete library for pedit and demo01")
cmake_minimum_required(VERSION 3.16.3)

# flags

# include files
include_directories( ./include )

# pkg-config calls
find_package(PkgConfig REQUIRED) 

pkg_check_modules(SDL2 REQUIRED IMPORTED_TARGET sdl2)
#pkg_check_modules(SDL2_MIXER REQUIRED IMPORTED_TARGET SDL2_mixer)
#pkg_check_modules(SDL2_GFX REQUIRED IMPORTED_TARGET SDL2_gfx)

#add_subdirectory(src)

#file(GLOB_RECURSE pedit_SOURCES "./src/*.c*")
#add_executable(pedit ${pedit_SOURCES})
# apparently, GLOB is evil

# Easy way to get list of files in vim
# :read ! ls src/*.cpp

add_library(akinopallete STATIC
    src/pallete.cpp
    )

target_link_libraries(akinopallete PUBLIC
    PkgConfig::SDL2
    )

# compile options
if (MSVC)
    # warning level 4 and all warnings as errors
    add_compile_options(/W4 /WX)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()
