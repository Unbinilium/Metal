cmake_minimum_required(VERSION 3.12.0)

set(CMAKE_CXX_STANDARD 17)

add_library(Metal INTERFACE)

find_library(APPLE_FWK_FOUNDATION Foundation REQUIRED)
find_library(APPLE_FWK_QUARTZ_CORE QuartzCore REQUIRED)
find_library(APPLE_FWK_METAL Metal REQUIRED)
find_library(APPLE_FWK_METAL_KIT MetalKit REQUIRED)
find_library(APPLE_FWK_APP_KIT AppKit REQUIRED)

target_include_directories(Metal INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/metal-cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/metal-cpp-extensions
)

target_compile_definitions(Metal INTERFACE
    NS_PRIVATE_IMPLEMENTATION
    CA_PRIVATE_IMPLEMENTATION
    MTL_PRIVATE_IMPLEMENTATION
    MTK_PRIVATE_IMPLEMENTATION
)

target_link_libraries(Metal INTERFACE
    ${APPLE_FWK_FOUNDATION}
    ${APPLE_FWK_QUARTZ_CORE}
    ${APPLE_FWK_METAL}
    ${APPLE_FWK_METAL_KIT}
    ${APPLE_FWK_APP_KIT}
)
