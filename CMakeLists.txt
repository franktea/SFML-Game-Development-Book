
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

# 定义build_chapter函数，每个章节的编译规则一样
function(build_chapter chapter_name SRC)
    add_executable(${chapter_name} ${SRC})

    target_include_directories(${chapter_name} PRIVATE ../Include)
    target_link_libraries(${chapter_name} PRIVATE
        sfml-graphics
        sfml-window
        sfml-audio
        sfml-network
        sfml-system
    )

	# 设置可执行文件输出路径
    set_target_properties(${chapter_name} PROPERTIES RUNTIME_OUTPUT_DIRECTORY
		${PROJECT_SOURCE_DIR}/binary/${chapter_name})

    add_custom_command(TARGET ${chapter_name} PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E make_directory
        ${PROJECT_SOURCE_DIR}/binary/${chapter_name}
    )

    # 拷贝资源目录
    add_custom_target(copy_data_${chapter_name}
        COMMAND ${CMAKE_COMMAND} -E copy_directory_if_different 
        "${PROJECT_SOURCE_DIR}/${chapter_name}/Media"
        "${PROJECT_SOURCE_DIR}/binary/${chapter_name}/Media"
        COMMENT "Copying data for ${chapter_name}"
    )
    add_dependencies(${chapter_name} copy_data_${chapter_name})
endfunction()

# C++ source code, list of all subdirectories
# Must appear after macros, otherwise they are not visible in subdirectories
#add_subdirectory(01_Intro/Source)
#add_subdirectory(02_Resources/Source)
add_subdirectory(03_World/Source)
#add_subdirectory(04_Input/Source)
#add_subdirectory(05_States/Source)
#add_subdirectory(06_Menus/Source)
#add_subdirectory(07_Gameplay/Source)
#add_subdirectory(08_Graphics/Source)
#add_subdirectory(09_Audio/Source)
#add_subdirectory(10_Network/Source)
