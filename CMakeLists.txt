cmake_minimum_required(VERSION 3.0)

project(imgui)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)
find_package(glfw3 3.3 REQUIRED)


include_directories(
        ${CMAKE_SOURCE_DIR}/
        ${CMAKE_SOURCE_DIR}/backends
        /opt/local/include
)

file(GLOB imgui_SRC
        ${CMAKE_SOURCE_DIR}/imgui.cpp
        ${CMAKE_SOURCE_DIR}/imgui_draw.cpp
        ${CMAKE_SOURCE_DIR}/imgui_widgets.cpp
        ${CMAKE_SOURCE_DIR}/imgui_tables.cpp
        ${CMAKE_SOURCE_DIR}/backends/imgui_impl_glfw.cpp
        ${CMAKE_SOURCE_DIR}/backends/imgui_impl_opengl2.cpp
        )


add_library(libImgui ${imgui_SRC})


add_executable(demo imgui_demo.cpp examples/example_glfw_opengl2/main.cpp)
target_link_libraries(demo libImgui glfw ${OPENGL_LIBRARIES})