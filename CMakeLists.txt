cmake_minimum_required(VERSION 3.15)
project(Calc--)

# Setup language requirements
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#--------------------------------------------------
# Add google test and setup build
#--------------------------------------------------
include(FetchContent)
FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG release-1.11.0
)

# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# No need for GMock
set(BUILD_GMOCK OFF CACHE BOOL "" FORCE)
set(INSTALL_GTEST OFF CACHE BOOL "" FORCE)
set(GTEST_FORCE_SHARED_CRT ON CACHE BOOL "" FORCE)
set(GTEST_DISABLE_PTHREADS ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

add_executable(Calc-- main.cpp)

include_directories(CalcLib)
add_subdirectory(CalcLib)
add_subdirectory(test)

target_link_libraries(Calc-- CalcLib)

if (MSVC)
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT CalcLib)
    set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT test)
endif ()

