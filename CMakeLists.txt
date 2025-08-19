cmake_minimum_required(VERSION 3.11)

project(nanovg C)

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

add_library(nanovg-static STATIC ${NANOVG_SOURCES} ${NANOVG_HEADERS})

add_subdirectory(example)