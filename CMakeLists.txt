cmake_minimum_required(VERSION 3.16)
project(MyProject LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(main
    src/main.cpp
)

target_include_directories(main
    PRIVATE ${PROJECT_SOURCE_DIR}/include
)

target_compile_options(main PRIVATE
    -Wall -Wextra -Wpedantic
)

# Testing
include(CTest)  # Automatically enables testing unless BUILD_TESTING=OFF

if(BUILD_TESTING)
    add_executable(test_main
        src/main.cpp
    )

    target_include_directories(test_main
        PRIVATE ${PROJECT_SOURCE_DIR}/include
    )

    target_compile_options(test_main PRIVATE
        -Wall -Wextra -Wpedantic
    )

    add_test(NAME smoke COMMAND test_main)
endif()
