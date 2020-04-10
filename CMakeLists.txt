cmake_minimum_required(VERSION 3.8)
project(gelato-sandbox CXX)
SET (PROJECT_SOURCE_DIR "${PROJECT_SOURCE_DIR}/source")
SET (GLFW_SOURCE_DIR "vendor/glfw-3.3")
SET (GELATO_PROJECT_DIR "gelato")

include_directories(${PROJECT_SOURCE_DIR})

# glfw 3.3
add_subdirectory(${GLFW_SOURCE_DIR})

# gelato
add_subdirectory(${GELATO_PROJECT_DIR})

# gelato-sandbox cpp application
add_executable(
    gelato-sandbox 
    ${PROJECT_SOURCE_DIR}/sandbox.cpp
    ${PROJECT_SOURCE_DIR}/stb_image.c
)
set_property(TARGET gelato-sandbox PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}")
target_include_directories(gelato-sandbox PRIVATE ${GLFW_SOURCE_DIR}/include PRIVATE ${GELATO_PROJECT_DIR}/source)
target_link_libraries(gelato-sandbox PUBLIC glfw ${GLFW_LIBRARIES} PRIVATE gelato)