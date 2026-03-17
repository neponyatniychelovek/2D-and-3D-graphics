cmake_minimum_required(VERSION 3.10)

project(ModelViewer)

find_package(OpenGL REQUIRED)

# Укажи путь к FreeGLUT
set(FREEGLUT_DIR "${CMAKE_SOURCE_DIR}/freeglut")
include_directories("${FREEGLUT_DIR}/include")

add_executable(ModelViewer main.cpp)

target_link_libraries(ModelViewer 
    opengl32 
    glu32 
    "${FREEGLUT_DIR}/lib/x64/freeglut.lib"
)

# --- КОПИРОВАНИЕ ФАЙЛОВ ---

# 1. Копируем DLL
add_custom_command(TARGET ModelViewer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${FREEGLUT_DIR}/bin/x64/freeglut.dll"
    $<TARGET_FILE_DIR:ModelViewer>
)

# 2. Копируем МОДЕЛЬ (model.obj)
add_custom_command(TARGET ModelViewer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${CMAKE_SOURCE_DIR}/model.obj"
    $<TARGET_FILE_DIR:ModelViewer>
)