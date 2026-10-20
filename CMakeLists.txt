cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
#----------------------------------------------------------------------------
# Setup the project, first we make sure the compiler is the one corresponding 
# to the ups e7 compiler.. 
#

project(g4hp C CXX)

#----------------------------------------------------------------------------
# Setup geant4 and root
#
find_package(Geant4 REQUIRED)
include(${Geant4_USE_FILE})
find_package(ROOT REQUIRED)

#----------------------------------------------------------------------------
# Locate sources and headers for this project
#
include_directories(${PROJECT_SOURCE_DIR}/include
		    ${Geant4_INCLUDE_DIR}
		    ${ROOT_INCLUDE_DIRS}
		    )

file(GLOB sources  ${PROJECT_SOURCE_DIR}/src/*.cc)
file(GLOB hheaders ${PROJECT_SOURCE_DIR}/include/*.hh)
file(GLOB headers  ${PROJECT_SOURCE_DIR}/include/*.h)

set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -g" )
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/build) # just for libg4hpDict.so
#----------------------------------------------------------------------------
#g4hpCint
#
add_custom_command(
    OUTPUT g4hpCint.cc 
    COMMAND rootcint -f g4hpCint.cc -c 
            ${PROJECT_SOURCE_DIR}/include/hptuple.hh 
            ${PROJECT_SOURCE_DIR}/include/TrackInfo_t.hh 
            ${PROJECT_SOURCE_DIR}/Linkdef.h
    DEPENDS 
            ${PROJECT_SOURCE_DIR}/include/hptuple.hh 
            ${PROJECT_SOURCE_DIR}/include/TrackInfo_t.hh 
            ${PROJECT_SOURCE_DIR}/Linkdef.h
)
add_library(g4hpDict SHARED g4hpCint.cc
	    ${PROJECT_SOURCE_DIR}/src/TrackInfo_t.cc 
	    ${PROJECT_SOURCE_DIR}/src/hptuple.cc )

#----------------------------------------------------------------------------
#Build g4hp
#
link_directories(${PROJECT_SOURCE_DIR}/build)
add_executable(g4hp g4hp.cc ${sources} ${headers} ${hheaders} ${physics} )
target_link_libraries(g4hp g4hpDict ${Geant4_LIBRARIES} ${ROOT_LIBRARIES} )

#----------------------------------------------------------------------------
# Install the executable to 'bin' directory under CMAKE_INSTALL_PREFIX
#
install(TARGETS g4hp  DESTINATION bin)

