cmake_minimum_required(VERSION 3.11)

project(nanovg C)

option(NVG_BUILD_GL_EXAMPLE "Build GL3 example" OFF])
option(NVG_BUILD_GLES_EXAMPLE "Build GLES example" OFF])
option(NVG_BUILD_WITH_MSAA "Build with MSAA on" OFF])
option(NVG_BUILD_SHARED "Build shared (dyanmic) library" OFF])

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

include_directories(src)


set(NANOVG_SOURCES
    src/nanovg.h
    src/nanovg.c
)

set(NANOVG_HEADERS
    src/fontstash.h
    src/nanovg_gl.h
    src/nanovg_gl_utils.h
    src/stb_image.h
    src/stb_truetype.h
)

if (${NVG_BUILD_SHARED})
    add_library(nanovg SHARED ${NANOVG_SOURCES} ${NANOVG_HEADERS})
endif()

add_library(nanovg-static STATIC ${NANOVG_SOURCES} ${NANOVG_HEADERS})

add_subdirectory(example)