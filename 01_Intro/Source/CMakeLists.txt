
set (SRC	
	Game.cpp
)

set(SRC ${SRC} Main.cpp)
add_executable(01_Intro ${SRC})
target_include_directories(01_Intro PRIVATE ../Include)
target_link_libraries(01_Intro PRIVATE
	sfml-graphics
	sfml-window
	sfml-audio
	sfml-network
	sfml-system
)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/binary/01_Intro)

add_custom_command(TARGET 01_Intro PRE_BUILD
	COMMAND ${CMAKE_COMMAND} -E make_directory
	${PROJECT_SOURCE_DIR}/binary/01_Intro)

# copy resource directory
add_custom_target(copy_data
	COMMAND ${CMAKE_COMMAND} -E copy_directory_if_different 
        "${CMAKE_CURRENT_SOURCE_DIR}/../Media"
        "$<TARGET_FILE_DIR:01_Intro>/Media"
    COMMENT "Copying data"
)
add_dependencies(01_Intro copy_data)

