cmake_minimum_required(VERSION 3.0)

project(imgui)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)

if (APPLE)
find_package(glfw3 3.3 REQUIRED)
endif()


include_directories(
        ${CMAKE_SOURCE_DIR}/
        ${CMAKE_SOURCE_DIR}/backends

)

if (APPLE)
    include_directories(
            /opt/local/include
    )
elseif (WIN32)
    include_directories(
            ${CMAKE_SOURCE_DIR}/examples/libs/glfw/include
    )
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MD")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
endif ()

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
target_link_libraries(demo libImgui ${OPENGL_LIBRARIES})

if (APPLE)
    target_link_libraries(demo glfw)
elseif (WIN32)
    target_link_libraries(demo ${CMAKE_SOURCE_DIR}/examples/libs/glfw/lib-vc2010-64/glfw3.lib)
endif ()