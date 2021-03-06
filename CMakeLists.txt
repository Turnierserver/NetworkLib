cmake_minimum_required(VERSION 3.1)
project("Turnierserver NetworkLib")

set(netlib_MAJOR 2)
set(netlib_MINOR 0)
set(netlib_PATCH 0)
set(netlib_VERSION ${netlib_MAJOR}.${netlib_MINOR}.${netlib_PATCH})

find_package(Qt5 5.5.0 REQUIRED COMPONENTS Core Network)
set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

if(CMAKE_COMPILER_IS_GNUCXX)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror=format -Werror=return-type")
endif()

if(CMAKE_BUILD_TYPE MATCHES Debug)
	if(CMAKE_COMPILER_IS_GNUCXX)
		set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -fsanitize=undefined")
	else()
		set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
	endif()
	add_definitions("-D_GLIBCXX_DEBUG")
	add_definitions("-DQT_SHAREDPOINTER_TRACK_POINTERS")
	add_definitions("-DCMAKE_DEBUG")
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

add_subdirectory(QtFtp)
