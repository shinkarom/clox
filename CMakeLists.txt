cmake_minimum_required(VERSION 3.13.2)

set(PROJ_NAME clox)
project(${PROJ_NAME} C)
set(EXE_NAME ${PROJ_NAME})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

include_directories(${CMAKE_SOURCE_DIR}/src)

add_executable(${PROJ_NAME}
	src/main.c
	src/chunk.c
	src/memory.c
	src/debug.c
	src/value.c
	src/vm.c
)

#target_link_libraries(${PROJ_NAME} )

set_target_properties(${PROJ_NAME} PROPERTIES
	LINKER_LANGUAGE C
)

target_compile_options(${EXE_NAME} PUBLIC 
	-g -Wall 
	$<$<CONFIG:Debug>:-g> 
	$<$<CONFIG:Release>: -O2>
)
target_link_options(${EXE_NAME} PUBLIC 
	$<$<CONFIG:RELEASE>: -s>
)
