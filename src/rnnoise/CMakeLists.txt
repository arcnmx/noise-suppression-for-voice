cmake_minimum_required(VERSION 3.6)
project(RnNoise LANGUAGES C)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

file(RN_NOISE_SRC rnnoise/src/*.c)

add_library(RnNoise STATIC ${RN_NOISE_SRC})

# Disable all warnings, since it's an external library.
target_compile_options(RnNoise PRIVATE
        $<$<OR:$<C_COMPILER_ID:Clang>,$<C_COMPILER_ID:AppleClang>,$<C_COMPILER_ID:GNU>>:
        -w>
        $<$<CXX_COMPILER_ID:MSVC>:
        /w>)

target_include_directories(RnNoise PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
        PRIVATE rnnoise/include)
