cmake_minimum_required(VERSION 3.20)
project(IGI-Offline-Trainer LANGUAGES CXX RC)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

add_executable(IGI-Offline-Trainer WIN32
    src/main.cpp
    src/App.cpp
    src/GameTrainer.cpp
    src/ProcessMemory.cpp
    resources/app.rc
)

target_include_directories(IGI-Offline-Trainer PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/resources
)

target_compile_definitions(IGI-Offline-Trainer PRIVATE
    UNICODE
    _UNICODE
    NOMINMAX  # <-- Prevents Windows.h from defining min/max macros
)

if(MSVC)
    target_compile_options(IGI-Offline-Trainer PRIVATE /utf-8)
endif()

target_link_libraries(IGI-Offline-Trainer PRIVATE
    d2d1
    dwrite
    dwmapi
    user32
    gdi32
    ole32
)

set_target_properties(IGI-Offline-Trainer PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)
