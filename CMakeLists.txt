################################################################################
cmake_minimum_required(VERSION 3.23.0)

################################################################################
# Project, Languages, Version
################################################################################
project(mbf-tp-pole LANGUAGES CXX VERSION 1.0.0)

################################################################################
# Source files
################################################################################

set (POLE_FILES_HDR
  pole.h)
  
set (POLE_FILES_SRC
  pole.cpp)


################################################################################
# Link libraries
################################################################################

add_library(${PROJECT_NAME} ${POLE_FILES_SRC})

#target_link_libraries(${PROJECT_NAME}
	#PRIVATE
		#none
	#PUBLIC
		#none
#)

################################################################################
# Header file set
################################################################################
target_sources(${PROJECT_NAME} PUBLIC
	FILE_SET public_headers
	TYPE HEADERS
	FILES ${POLE_FILES_HDR}
)

################################################################################
# Build include directories
################################################################################
target_include_directories(${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")

################################################################################
# Install target
################################################################################
install(TARGETS ${PROJECT_NAME}
		EXPORT ${PROJECT_NAME}-targets
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
		FILE_SET public_headers DESTINATION "include/pole"
)

################################################################################
# Export and install cmake configuration files
################################################################################
export(TARGETS ${PROJECT_NAME}
    NAMESPACE ${PROJECT_NAME}::
    FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
)

install(EXPORT ${PROJECT_NAME}-targets
	FILE "${PROJECT_NAME}Config.cmake"
	NAMESPACE ${PROJECT_NAME}::
    DESTINATION "share/${PROJECT_NAME}"
)
