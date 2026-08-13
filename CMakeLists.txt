cmake_minimum_required(VERSION 3.25)

project(ISaidNoRTTI
    VERSION 1.0
    LANGUAGES CXX
)

# ============================================================
# C++ configuration
# ============================================================

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# ============================================================
# Source files
# ============================================================

set(ISAIDNORTTI_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/ISaidNoRTTI.cpp"
)

# ============================================================
# Target
# ============================================================

add_executable(ISaidNoRTTI
    ${ISAIDNORTTI_SOURCES}
)

# ============================================================
# Compiler configuration
# ============================================================

if(MSVC)

    # Microsoft Visual C++ / clang-cl
    target_compile_options(ISaidNoRTTI PRIVATE
        /W3
        /EHsc
    )

    target_compile_options(ISaidNoRTTI PRIVATE
        $<$<CONFIG:Release>:/O2>
        $<$<CONFIG:Debug>:/Od>
        $<$<CONFIG:Debug>:/Zi>
    )

elseif(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")

    # Clang / LLVM
    target_compile_options(ISaidNoRTTI PRIVATE
        -Wall
        -Wextra
        -Wpedantic
    )

    target_compile_options(ISaidNoRTTI PRIVATE
        $<$<CONFIG:Release>:-O2>
        $<$<CONFIG:Debug>:-O0>
        $<$<CONFIG:Debug>:-g>
    )

elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")

    # Optional GCC support
    target_compile_options(ISaidNoRTTI PRIVATE
        -Wall
        -Wextra
        -Wpedantic
    )

    target_compile_options(ISaidNoRTTI PRIVATE
        $<$<CONFIG:Release>:-O2>
        $<$<CONFIG:Debug>:-O0>
        $<$<CONFIG:Debug>:-g>
    )

endif()

# ============================================================
# Output
# ============================================================

set_target_properties(ISaidNoRTTI PROPERTIES
    OUTPUT_NAME "ISaidNoRTTI"

    RUNTIME_OUTPUT_DIRECTORY
        "${CMAKE_CURRENT_SOURCE_DIR}/bin/$<CONFIG>"
)

# ============================================================
# Status
# ============================================================

message(STATUS "")
message(STATUS "========================================")
message(STATUS " ISaidNoRTTI")
message(STATUS "========================================")
message(STATUS "Compiler ID   : ${CMAKE_CXX_COMPILER_ID}")
message(STATUS "Compiler      : ${CMAKE_CXX_COMPILER}")
message(STATUS "Version       : ${CMAKE_CXX_COMPILER_VERSION}")
message(STATUS "C++ standard  : C++${CMAKE_CXX_STANDARD}")
message(STATUS "Source        : ${CMAKE_CURRENT_SOURCE_DIR}/src")
message(STATUS "Output        : ${CMAKE_CURRENT_SOURCE_DIR}/bin/$<CONFIG>")
message(STATUS "========================================")
message(STATUS "")