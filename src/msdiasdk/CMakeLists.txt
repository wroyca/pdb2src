file(GLOB_RECURSE msdiasdk RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.cpp *.hpp)

add_executable(msdiasdk
    ${msdiasdk}
)

target_compile_options(msdiasdk
PRIVATE
    /Oi # Replaces some function calls with intrinsic.
    /Ot # Instruct the compiler to favor speed over size.
)

target_include_directories(msdiasdk
PRIVATE
    "C:/Program Files/Microsoft Visual Studio/2022/Preview/DIA SDK/include"
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_directories(msdiasdk
PRIVATE
    "C:/Program Files/Microsoft Visual Studio/2022/Preview/DIA SDK/lib/amd64"
)

target_link_libraries(msdiasdk
PRIVATE
    diaguids
)

target_precompile_headers(msdiasdk
PRIVATE
    stdafx.hpp
)

target_create_virtual_directories(msdiasdk)
