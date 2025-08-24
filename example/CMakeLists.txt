set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

file(COPY ${PROJECT_SOURCE_DIR}/example/images DESTINATION ${PROJECT_BINARY_DIR}/example)

file(GLOB TTF_FILES
    "${PROJECT_SOURCE_DIR}/example/*.ttf"
)

file(COPY ${TTF_FILES} DESTINATION ${PROJECT_BINARY_DIR}/example)

if(WIN32)
    set(NVG_EXTRA_LIBS opengl32)
elseif(APPLE)
    set(NVG_EXTRA_LIBS "-framework OpenGL" dl m)
elseif(MSYS)
    set(NVG_EXTRA_LIBS mingw32 winmm pthread m)
elseif(UNIX)
    set(NVG_EXTRA_LIBS pthread GL dl m)
else()
    message(FATAL_ERROR "Unsupported operating system.")
endif()

if (${NVG_BUILD_GL3_EXAMPLE})
    add_executable(example_gl3 example_gl3.c demo.c perf.c)
    target_link_libraries(example_gl3 nanovg-static glfw ${NVG_EXTRA_LIBS})

    if (${NVG_BUILD_WITH_MSAA})
        target_compile_definitions(example_gl3 PRIVATE DEMO_MSAA)
    endif()
endif()

if (${NVG_BUILD_GLES3_EXAMPLE})
    add_executable(example_gles3 example_gles3.c demo.c perf.c)
    target_link_libraries(example_gles3 nanovg-static glfw ${NVG_EXTRA_LIBS})
    target_compile_definitions(example_gles3 PRIVATE NANOVG_TIMER_EXT)
endif()

if (${NVG_BUILD_FBO_EXAMPLE})
    add_executable(example_fbo example_fbo.c demo.c perf.c)
    target_link_libraries(example_fbo nanovg-static glfw ${NVG_EXTRA_LIBS})
    target_compile_definitions(example_fbo PRIVATE NANOVG_TIMER_EXT)

    if (${NVG_BUILD_WITH_MSAA})
        target_compile_definitions(example_fbo PRIVATE DEMO_MSAA)
    endif()
endif()
