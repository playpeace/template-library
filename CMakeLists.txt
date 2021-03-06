cmake_minimum_required(VERSION 3.4)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake_modules)

# Project name and version
project(template-library VERSION 0.1.0 LANGUAGES CXX)

# Use a pkg-config module for CMake
find_package(PkgConfig)

# Define GNU standard installation directories
include(GNUInstallDirs)

# C++ compiler flags
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_EXTENSIONS OFF)

# Project targets
set(TARGET ${PROJECT_NAME})

# Target source files
include_directories(src include)
file(GLOB SOURCE_FILES      "src/*.cpp" "src/*.h")
file(GLOB PUBLIC_HEADERS    "include/*.h")

# Declare library
add_library(${TARGET} SHARED ${SOURCE_FILES} ${PUBLIC_HEADERS})

# Create pkgconfig file
configure_file(template-library.pc.in template-library.pc @ONLY)

# Install directives
install(FILES ${PUBLIC_HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${TARGET})
install(TARGETS ${TARGET} DESTINATION ${CMAKE_INSTALL_LIBDIR})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/template-library.pc DESTINATION ${CMAKE_INSTALL_LIBDIR}/pkgconfig)

enable_testing()
add_subdirectory(tests)
