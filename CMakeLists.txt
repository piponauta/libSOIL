cmake_minimum_required(VERSION 3.12)

find_package(OpenGL REQUIRED)

set(LIBSOIL_SOURCES
    image_DXT.c
    image_helper.c
    SOIL.c
    stb_image_aug.c
)

set(LIBSOIL_HEADERS
    image_DXT.h
    image_helper.h
    SOIL.h
    stb_image_aug.h
    stbi_DDS_aug.h
    stbi_DDS_aug_c.h
)

if(BUILD_LIBSOIL_STATIC)
    set(LIBSOIL_TYPE SHARED)
else()
    set(LIBSOIL_TYPE STATIC)
endif()

add_library(SOIL ${LIBSOIL_TYPE}
    ${LIBSOIL_SOURCES}
    ${LIBSOIL_HEADERS}
)
target_include_directories(SOIL PRIVATE OpenGL::GL)
if(NOT APPLE)
    target_include_directories(SOIL PRIVATE OpenGL::GLX)
endif()
set_target_properties(SOIL PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}")
