cmake_minimum_required(VERSION 3.13.2)

set(PROJ_NAME cmakeproj_cpp)
project(${PROJ_NAME} CXX)
set(EXE_NAME ${PROJ_NAME})

set(S ${CMAKE_BINARY_DIR}/..)

include_directories(${S}/src)

file(GLOB SRCS ${S}/src/*.cpp ${S}/src/*.c ${S}/src/*.cxx)
file(GLOB HS ${S}/src/*.hpp ${S}/src/*.h)

add_executable(${PROJ_NAME} ${SRCS} ${HS})

add_custom_command(TARGET ${PROJ_NAME} POST_BUILD
	COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:${PROJ_NAME}> ${S}/bin
)

#target_link_libraries(${PROJ_NAME} )

#set_target_properties(${PROJ_NAME} PROPERTIES
#	
#)

target_compile_options(${EXE_NAME} PUBLIC 
	-g -std=c++20 -Wall 
	$<$<CONFIG:Debug>:-g> 
	$<$<CONFIG:Release>: -O2>
)
target_link_options(${EXE_NAME} PUBLIC 
	$<$<CONFIG:RELEASE>: -s>
)
