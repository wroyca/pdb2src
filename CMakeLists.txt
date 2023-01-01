cmake_minimum_required(VERSION 3.23)
project(msdiasdk LANGUAGES CXX)

# Enables hooks that run automatically every time a particular .git event occurs.
if(CMAKE_GIT_HOOKS)
    file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/hooks/pre-commit DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/.git/hooks)
endif()

# Updates all submodules recursively along with their tracking branches.
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
    if(CMAKE_CHECKOUT_SUBMODULES)
        message(STATUS "Running git submodule update --init --recursive, please wait.")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} RESULT_VARIABLE RESULT)
        if(NOT RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init --recursive failed with ${GIT_SUBMOD_RESULT}, please checkout submodules.")
        endif()
    endif()
endif()

# Create virtual directories relative to the target source directory in Visual Studio.
function(target_create_virtual_directories target_name)
    if(CMAKE_VIRTUAL_DIRECTORIES)
        get_target_property(target_sources  "${target_name}" SOURCES)
        foreach(file_name IN LISTS target_sources)
            get_filename_component(dir_name "${file_name}" PATH)
            string(REPLACE "/" "\\" group_name "${dir_name}")
            source_group("${group_name}" FILES "${file_name}")
        endforeach()
    endif()
endfunction()

add_definitions(-DCMAKE_INSTALL_PREFIX="${CMAKE_INSTALL_PREFIX}/")
add_definitions(-DCMAKE_BINARY_DIR="${CMAKE_BINARY_DIR}/src/msdiasdk/Debug/")

add_subdirectory(src)
