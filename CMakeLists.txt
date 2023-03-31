cmake_minimum_required(VERSION 3.18)
project(SYSY-RPG)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED true)


add_compile_options(
	-g -Wall -Werror -Wextra -pthread
	-Wno-unused-parameter
	-Wno-unused-variable
	-Wno-unknown-pragmas
)
add_link_options(-lpthread -lm -v -pthread)

add_executable(
	sysy-rpg
	src/main.cpp
)
