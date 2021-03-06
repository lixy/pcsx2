# Check that people use the good file
if(NOT TOP_CMAKE_WAS_SOURCED)
    message(FATAL_ERROR "
    You did not 'cmake' the good CMakeLists.txt file. Use the one in the top dir.
    It is advice to delete all wrongly generated cmake stuff => CMakeFiles & CMakeCache.txt")
endif()


# plugin name
set(Output onepad-1.1.0)

set(OptimizationFlags
    -O2
    )

if(CMAKE_BUILD_TYPE STREQUAL Debug)
    set(onepadFinalFlags "")

elseif(CMAKE_BUILD_TYPE STREQUAL Devel)
	set(onepadFinalFlags ${OptimizationFlags})

elseif(CMAKE_BUILD_TYPE STREQUAL Release)
	set(onepadFinalFlags ${OptimizationFlags})

endif()

# onepad sources
set(onepadSources
	controller.cpp
	joystick.cpp
	keyboard.cpp
    KeyStatus.cpp
	onepad.cpp)

# onepad headers
set(onepadHeaders
	bitwise.h
	controller.h
	joystick.h
	keyboard.h
    KeyStatus.h
	onepad.h)

# onepad Linux sources
set(onepadLinuxSources
	Linux/ini.cpp
	Linux/dialog.cpp
	Linux/linux.cpp)

# onepad Linux headers
set(onepadLinuxHeaders
	Linux/linux.h)

# onepad Windows sources
set(onepadWindowsSources
	)

# onepad Windows headers
set(onepadWindowsHeaders
	)

if (SDL2_API)
	set(onepadFinalLibs
		${SDL2_LIBRARIES}
	)
else()
	set(onepadFinalLibs
		${SDL_LIBRARY}
	)
endif()

set(onepadFinalLibs
	${onepadFinalLibs}
	${GTK2_LIBRARIES}
	${X11_LIBRARIES}
)

set(onepadFinalSources
	${onepadSources}
	${onepadHeaders}
	${onepadLinuxSources}
	${onepadLinuxHeaders}
)

add_pcsx2_plugin(${Output} "${onepadFinalSources}" "${onepadFinalLibs}" "${onepadFinalFlags}")
