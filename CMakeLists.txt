cmake_minimum_required(VERSION 3.10)
project(Ragify)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Main executable
add_executable(ragify main.cpp)

# Link Windows socket libraries (Windows only)
if(WIN32)
    target_link_libraries(ragify ws2_32 wsock32)
endif()

# Compiler optimizations
if(MSVC)
    target_compile_options(ragify PRIVATE /O2 /W4)
else()
    target_compile_options(ragify PRIVATE -O2 -Wall -Wextra)
endif()

# Installation
install(TARGETS ragify DESTINATION bin)
install(FILES index.html DESTINATION bin)
