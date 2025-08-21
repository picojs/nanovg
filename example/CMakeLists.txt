set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

file(COPY ${PROJECT_SOURCE_DIR}/example/images DESTINATION ${PROJECT_BINARY_DIR}/example)

file(GLOB TTF_FILES
    "${PROJECT_SOURCE_DIR}/example/*.ttf"
)

file(COPY ${TTF_FILES} DESTINATION ${PROJECT_BINARY_DIR}/example)

include_directories(../src)

if (${NVG_BUILD_GL3_EXAMPLE})
    add_executable(example_gl3 example_gl3.c demo.c perf.c)
    target_link_libraries(example_gl3 nanovg-static glfw GL m)
    target_compile_options(example_gl3 PRIVATE -g -Wall -Wextra)
endif()

if (${NVG_BUILD_GL3_EXAMPLE} AND ${NVG_BUILD_WITH_MSAA})
    add_executable(example_gl3_msaa example_gl3.c demo.c perf.c)
    target_link_libraries(example_gl3_msaa nanovg-static glfw GL m)
    target_compile_definitions(example_gl3_msaa PRIVATE DEMO_MSAA)
endif()

if (${NVG_BUILD_GLES3_EXAMPLE})
    add_executable(example_gles3 example_gles3.c demo.c perf.c)
    target_link_libraries(example_gles3 nanovg-static glfw GL m)
    target_compile_options(example_gles3 PRIVATE -g -Wall -Wextra)
    target_compile_definitions(example_gles3 PRIVATE NANOVG_GLES3)
endif()