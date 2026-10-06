cmake_minimum_required(VERSION 3.28)
project(stardancer LANGUAGES CXX)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 3.1.0
    GIT_SHALLOW ON
    EXCLUDE_FROM_ALL
    SYSTEM)
FetchContent_MakeAvailable(SFML)

file(COPY ${CMAKE_SOURCE_DIR}/src/assets/
     DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/src/assets)

if(NOT EXISTS "${CMAKE_SOURCE_DIR}/src/assets/AldotheApache.ttf")
    message(FATAL_ERROR "Font file not found at src/assets/AldotheApache.ttf")

endif()

add_executable(stardancer src/main.cpp src/players.cpp)
target_compile_features(stardancer PRIVATE cxx_std_17)
target_link_libraries(stardancer PRIVATE SFML::Graphics SFML::Audio SFML::System SFML::Window)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT stardancer)

add_custom_command(
    TARGET stardancer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${CMAKE_SOURCE_DIR}/src/assets"
        "$<TARGET_FILE_DIR:stardancer>"
    COMMENT ""
)