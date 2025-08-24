cmake_minimum_required(VERSION 3.11)

project(nanovg C)

option(NVG_BUILD_GL3_EXAMPLE "Build GL3 example" OFF])
option(NVG_BUILD_GLES3_EXAMPLE "Build GLES example" OFF])
option(NVG_BUILD_FBO_EXAMPLE "Build FBO example" ON])
option(NVG_BUILD_WITH_MSAA "Build with MSAA on" OFF])
option(NVG_BUILD_SHARED "Build shared (dyanmic) library" OFF])
option(NVG_INSTALL "Generate install targets" OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

set(NANOVG_SOURCES
    ./src/nanovg.c
)

set(NANOVG_HEADERS
    ./include/nanovg.h
    ./include/nanovg_gl.h
    ./src/fontstash.h
    ./src/stb_image.h
    ./src/stb_truetype.h
)

if (${NVG_BUILD_SHARED})
    add_library(nanovg SHARED ${NANOVG_SOURCES} ${NANOVG_HEADERS})
    target_include_directories(nanovg PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
    )
endif()

add_library(nanovg-static STATIC ${NANOVG_SOURCES} ${NANOVG_HEADERS})

target_include_directories(nanovg-static PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

add_subdirectory(example)

if (${NVG_INSTALL})
    install(DIRECTORY include DESTINATION include)
    install(TARGETS nanovg-static DESTINATION lib)

    if(NVG_BUILD_SHARED)
        install(TARGETS nanovg DESTINATION lib)
    endif()
endif()