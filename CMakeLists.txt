# Your desired CMake version. Please check currently installed with `cmake --version`
cmake_minimum_required(VERSION 3.20.1)
# Your project name and version
project(SDL2_LOVES_CMAKE VERSION 1.1)
# C++ standard project uses
set(CMAKE_CXX_STANDARD 20)
# Creates config file
configure_file(SDL2_LOVES_CMAKEConfig.hpp.in SDL2_LOVES_CMAKEConfig.hpp)
# Create executable
add_executable(${PROJECT_NAME} main.cpp)
# Include binary dir
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})

# Download submodules. This will automatically get all submodules
find_package(Git QUIET)
if (GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
    # Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if (GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if (NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "Git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif ()
    endif ()
endif ()

# Check all submodules
if (NOT EXISTS "${PROJECT_SOURCE_DIR}/ext/SDL2/CMakeLists.txt")
    message(FATAL_ERROR "The SDL2 submodule was not downloaded! GIT_SUBMODULE was turned off or failed. Please re-add")
endif ()

# Adds SDL2
add_subdirectory(ext/SDL2)
target_include_directories(${PROJECT_NAME} 
    PUBLIC ext/SDL2/include
)  
target_link_directories(${PROJECT_NAME} 
    PRIVATE ext/SDL2/src
)
target_link_libraries(${PROJECT_NAME} 
    SDL2
)