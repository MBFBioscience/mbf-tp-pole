################################################################################
cmake_minimum_required(VERSION 3.23.0...3.28.1)

project(pole LANGUAGES CXX VERSION 1.0.0)

set (POLE_FILES_HDR
  pole.h)
  
set (POLE_FILES_SRC
  pole.cpp)

add_library(${PROJECT_NAME} OBJECT ${POLE_FILES_SRC})

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
target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

################################################################################
# Install
################################################################################
install(TARGETS ${PROJECT_NAME} 
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
		FILE_SET public_headers DESTINATION "include/pole"
)
