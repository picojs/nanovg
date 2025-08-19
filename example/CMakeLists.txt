file(COPY ${PROJECT_SOURCE_DIR}/example/images DESTINATION ${PROJECT_BINARY_DIR}/example)

file(GLOB TTF_FILES
    "${PROJECT_SOURCE_DIR}/example/*.ttf"
)

file(COPY ${TTF_FILES} DESTINATION ${PROJECT_BINARY_DIR}/example)

include_directories(../src)

add_executable(example_gl3 example_gl3.c demo.c perf.c)
target_link_libraries(example_gl3 nanovg-static glfw GL m)
target_compile_options(example_gl3 PRIVATE -g -Wall -Wextra)