cmake_minimum_required (VERSION 3.13)

project (cpp-template LANGUAGES C CXX)

macro (add_source)
    file (RELATIVE_PATH _relPath "${PROJECT_SOURCE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}")
    foreach (_src ${ARGN})
        if (_relPath)
            list (APPEND SRCS "${_relPath}/${_src}")
        else()
            list (APPEND SRCS "${_src}")
        endif()
    endforeach()
    if (_relPath)
        set (SRCS ${SRCS} PARENT_SCOPE)
    endif()
endmacro()

add_subdirectory (src)

add_executable (cpp-template ${SRCS})
target_compile_options (cpp-template PRIVATE -Wall -Werror -rdynamic)
