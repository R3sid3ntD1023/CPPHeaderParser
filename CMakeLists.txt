cmake_minimum_required(VERSION 3.8)

message(STATUS "CMake version: ${CMAKE_VERSION}")

project(CPPParser LANGUAGES CSharp)
include(CSharpUtilities)

message(STATUS "Configuring CPPHeaderParser...")

file(GLOB_RECURSE SRC CMAKE_CONFIGURE_DEPENDS src/*.cs)

set(PROJECT_NAME CppHeaderParser)
set(DOTNET_TARGET_FRAMEWORK "v4.7.2")
set(CMAKE_CSharp_FLAGS "/langversion:latest")

add_executable(${PROJECT_NAME} ${SRC})
set_target_properties(${PROJECT_NAME} PROPERTIES 
    VS_DOTNET_TARGET_FRAMEWORK_VERSION ${DOTNET_TARGET_FRAMEWORK}
    VS_DOTNET_REFERENCES  "System"; "System.IO" ; "System.Text.RegularExpressions"
    CMAKE_CSharp_COMPILER ${CMAKE_CSharp_FLAGS}
    LINKER_LANGUAGE CSharp
    CMAKE_WIN32_EXECUTABLE TRUE
    VS_DOTNET_REFERENCES_PATH "${CMAKE_CURRENT_SOURCE_DIR}/lib")
