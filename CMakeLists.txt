cmake_minimum_required(VERSION 3.15)
project(Nuklear_D3D11_CMake LANGUAGES CXX)

add_library(Nuklear_D3D11_CMake STATIC
        src/nuklear/nuklear.h
        src/nuklear/nuklear_d3d11.h
        src/nuklear/nuklear_d3d11.hlsl
        src/nuklear/nuklear_d3d11_pixel_shader.h
        src/nuklear/nuklear_d3d11_vertex_shader.h
        src/nuklear/nuklear_d3d11.cpp
)

target_include_directories(Nuklear_D3D11_CMake PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:include>
)

set_target_properties(Nuklear_D3D11_CMake PROPERTIES
        C_STANDARD 11
        PUBLIC_HEADER "src/nuklear/nuklear.h;src/nuklear/nuklear_d3d11.h"
)

target_link_libraries(Nuklear_D3D11_CMake PRIVATE d3d11)

install(TARGETS Nuklear_D3D11_CMake
        EXPORT NuklearTargets
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin
        PUBLIC_HEADER DESTINATION include/nuklear
)

install(EXPORT NuklearTargets
        FILE NuklearTargets.cmake
        NAMESPACE Nuklear::
        DESTINATION lib/cmake/Nuklear
)

install(DIRECTORY src/nuklear/
        DESTINATION include/nuklear
        FILES_MATCHING PATTERN "*.h"
)
