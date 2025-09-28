cmake_minimum_required(VERSION 3.16)
project(ImGui)

# ImGui source files
set(IMGUI_SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imgui_tables.cpp
    imgui_demo.cpp        # optional
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_opengl3.cpp
)

# ImGui include directories
set(IMGUI_INCLUDES
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# Create static library
add_library(ImGui STATIC ${IMGUI_SOURCES})
target_include_directories(ImGui PUBLIC ${IMGUI_INCLUDES})

# C++17 standard
target_compile_features(ImGui PUBLIC cxx_std_17)

# Platform defines
if(WIN32)
    target_compile_definitions(ImGui PUBLIC _CRT_SECURE_NO_WARNINGS)
endif()

# ----------------------------
# Add dependency includes
# ----------------------------
# You must pass GLFW include dir to ImGui
target_include_directories(ImGui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/../GLFW/include   # adjust path if needed
)

# Link libraries if needed (optional)
# target_link_libraries(ImGui PUBLIC glfw OpenGL::GL)
