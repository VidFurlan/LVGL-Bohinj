cmake_minimum_required(VERSION 3.12)
project(lvgl_main)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)

find_package(SDL2 REQUIRED SDL2)
include_directories(
    ${SDL2_INCLUDE_DIRS}
    ${SDL2_INCLUDE_DIRS}/../

    ${CMAKE_SOURCE_DIR}/include/

    ${PROJECT_SOURCE_DIR}/config/
)

set(SOURCES
    src/main.cpp
)

set (FONTS
    fonts/montserrat_regular_40.c
    fonts/montserrat_bold_40.c
)

# Add lvgl sources
add_subdirectory(${PROJECT_SOURCE_DIR}/lib/lvgl)
add_subdirectory(${PROJECT_SOURCE_DIR}/lib/lv_drivers)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

add_executable(${PROJECT_NAME} ${FONTS} ${SOURCES} ${INCLUDES})
target_link_libraries(${PROJECT_NAME} PRIVATE lvgl lvgl::drivers ${SDL2_LIBRARIES})
add_custom_target(run COMMAND ${EXECUTABLE_OUTPUT_PATH}/${PROJECT_NAME})
