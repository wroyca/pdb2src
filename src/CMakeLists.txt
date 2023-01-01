# Global scope for vcxprojs headers.
include_directories(.)

# Global settings for the vcxprojs in solution.
add_compile_options(
    /MP                     # Build with multiple processes.
    $<$<CONFIG:Debug>:/Zi>  # The /Zi option produces a separate PDB file that contains all the symbolic debugging information.
)

add_definitions(
    /FI"stdafx.hpp"
)

add_subdirectory(msdiasdk)
