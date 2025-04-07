cmake_minimum_required(VERSION 3.30)
project(VulanEngine)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(/usr/local/include)
link_directories(/usr/local/lib)

find_library(COCOA_LIBRARY Cocoa)
find_library(IOKit_LIBRARY IOKit)
find_library(CoreVideo_LIBRARY CoreVideo)
find_package(Vulkan REQUIRED)
mark_as_advanced(COCOA_LIBRARY Vulkan)

find_package(glm REQUIRED)

SET(APPLE_LIBS ${COCOA_LIBRARY} ${IOKit_LIBRARY} ${CoreVideo_LIBRARY})

include_directories("include/Engine")

file(GLOB_RECURSE app_source_entry "src/entry/*.c*")
file(GLOB_RECURSE app_source_graphic "src/Engine/*.c*")

file(GLOB_RECURSE app_header_graphic "include/Engine/*.h*")

add_executable(${PROJECT_NAME} ${app_header_graphic} ${app_source_graphic} ${app_source_entry})

target_link_libraries(${PROJECT_NAME} ${APPLE_LIBS})
target_link_libraries(${PROJECT_NAME} glm::glm)
target_link_libraries(${PROJECT_NAME} glfw)
target_link_libraries(${PROJECT_NAME} vulkan)
