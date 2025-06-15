cmake_minimum_required(VERSION 3.10)
project(Pacman)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find SFML
find_package(SFML 2.5 COMPONENTS graphics window system REQUIRED)

# Add source files
set(SOURCES
    Source/Main.cpp
    Source/Pacman.cpp
    Source/Ghost.cpp
    Source/GhostManager.cpp
    Source/MapCollision.cpp
    Source/DrawText.cpp
    Source/DrawMap.cpp
    Source/ConvertSketch.cpp
)

# Create executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link SFML libraries
target_link_libraries(${PROJECT_NAME} sfml-graphics sfml-window sfml-system)

# Include header files directory
target_include_directories(${PROJECT_NAME} PRIVATE Source)

# Copy Resources directory to build directory
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/Resources $<TARGET_FILE_DIR:${PROJECT_NAME}>/Resources
)
