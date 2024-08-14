
cmake_minimum_required(VERSION 3.20)

set(CMAKE_CXX_STANDARD 20)

# Project name
project(sfml-book)

set(BUILD_SHARED_LIBS OFF)

include(FetchContent)
FetchContent_Declare(
	SFML
	GIT_REPOSITORY https://github.com/SFML/SFML.git
	GIT_TAG 2.6.1
)
FetchContent_MakeAvailable(SFML)

# C++ source code, list of all subdirectories
# Must appear after macros, otherwise they are not visible in subdirectories
add_subdirectory(01_Intro/Source)
#add_subdirectory(02_Resources/Source)
#add_subdirectory(03_World/Source)
#add_subdirectory(04_Input/Source)
#add_subdirectory(05_States/Source)
#add_subdirectory(06_Menus/Source)
#add_subdirectory(07_Gameplay/Source)
#add_subdirectory(08_Graphics/Source)
#add_subdirectory(09_Audio/Source)
#add_subdirectory(10_Network/Source)
