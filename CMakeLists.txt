cmake_minimum_required(VERSION 3.7.0)
project(Skeleton)

set(CMAKE_CXX_STANDARD 20)

set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

set(CMAKE_COLOR_MAKEFILE ON)
set(CMAKE_VERBOSE_MAKEFILE ON)

if (WIN32)
elseif (APPLE)
    # Architecture
    add_compile_options(-m64)
    # SSSE3 is the safest baseline for any arbitrary OSX release.
    add_compile_options(-mssse3)
    # Optimizations
    add_compile_options(-Ofast)
    # Warnings
    add_compile_options(-Wall)
    add_compile_options(-Wextra)
    set(CMAKE_CXX_VISIBILITY_PRESET hidden)
endif ()

add_subdirectory(extern)

set(
        PLUGIN_FOLDER
        "C:/Program Files/Adobe/Adobe After Effects 2023/Support Files/Plug-ins/"
        CACHE
        STRING
        "After Effects Plugin folder"
)


add_custom_command(
        OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rr
        COMMAND cl.exe /I \"${AESDK_ROOT}/Headers\" /EP \"${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}PiPL.r\" > ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rr
)

add_custom_command(
        DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rr
        OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rrc
        COMMAND ${AFX_REZ} ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rr ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rrc
)

add_custom_command(
        DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rrc
        OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rc
        COMMAND cl.exe /D "MSWindows" /EP ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rrc > ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rc
)


add_library(
        ${PROJECT_NAME}
        MODULE
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}PiPL.rc
        source/Skeleton.cpp
        source/Skeleton_Strings.cpp
)

target_include_directories(
        ${PROJECT_NAME}
        PRIVATE
        include
)


target_link_libraries(
        ${PROJECT_NAME}
        AESDK
)

install(
        TARGETS ${PROJECT_NAME}
        DESTINATION ${PLUGIN_FOLDER}
)


if (WIN32)
    set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX ".aex")
elseif (APPLE)
endif ()


