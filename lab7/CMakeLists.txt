cmake_minimum_required(VERSION 3.10)

project(FireSystem)

find_package(OpenGL REQUIRED)

# Укажи путь к FreeGLUT
set(FREEGLUT_DIR "${CMAKE_SOURCE_DIR}/freeglut")
include_directories("${FREEGLUT_DIR}/include")

add_executable(FireSystem main.cpp)

target_link_libraries(FireSystem 
    opengl32 
    glu32 
    "${FREEGLUT_DIR}/lib/x64/freeglut.lib"
)

# Копируем DLL
add_custom_command(TARGET FireSystem POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${FREEGLUT_DIR}/bin/x64/freeglut.dll"
    $<TARGET_FILE_DIR:FireSystem>
)