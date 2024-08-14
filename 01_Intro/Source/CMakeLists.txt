
set (SRC	
	Game.cpp
	Main.cpp
)

add_executable(01_Intro ${SRC})
target_include_directories(01_Intro PRIVATE ../Include)
target_link_libraries(01_Intro PRIVATE
	sfml-graphics
	sfml-window
	sfml-audio
	sfml-network
	sfml-system
)
