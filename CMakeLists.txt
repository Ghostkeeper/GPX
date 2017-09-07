project(GPX)
cmake_minimum_required(VERSION 3.2.3) #Only version it's tested with.

#Project metadata.
set(PACKAGE_NAME GPX CACHE STRING "The full name of this package.")
set(PACKAGE_VERSION 2.6.0 CACHE STRING "The version of this package.")
set(PACKAGE_BUGREPORT "https://github.com/markwal/GPX/issues" CACHE STRING "The address where bug reports for this package should be sent.")
set(PACKAGE_URL "https://github.com/markwal/GPX" CACHE STRING "The home page for this package.")
set(PACKAGE_TARNAME gpx CACHE STRING "The one symbol short name of this package.")

#Where to find the source code.
set(source_files
	src/gpx/gpx-main.c
	src/gpx/gpx.c
	src/gpx/gpxresp.c
	src/gpx/vector.c
	src/shared/machine_config.c
	src/shared/opt.c
	src/shared/s3g.c
	src/shared/s3g_stdio.c
)
if(WIN32)
	list(APPEND source_files src/gpx/winsio.c)
endif()
set(header_directories
	src
	src/gpx
	src/shared
)
include_directories(${CMAKE_CURRENT_BINARY_DIR} ${header_directories})

#Generate a config.h file in the same way that Autotool creates it.
include(CheckFunctionExists)
include(CheckIncludeFiles)
include(CheckTypeSize)
check_function_exists(atexit HAVE_ATEXIT)
check_include_files(fcntl.h HAVE_FCNTL_H)
check_include_files(float.h HAVE_FLOAT_H)
check_include_files(inttypes.h HAVE_INTTYPES_H)
check_include_files(limits.h HAVE_LIMITS_H)
check_function_exists(memmove HAVE_MEMMOVE)
check_include_files(memory.h HAVE_MEMORY_H)
check_function_exists(memset HAVE_MEMSET)
check_function_exists(nanosleep HAVE_NANOSLEEP)
check_function_exists(select HAVE_SELECT)
check_function_exists(sqrt HAVE_SQRT)
check_include_files(stdint.h HAVE_STDINT_H)
check_include_files(stdlib.h HAVE_STDLIB_H)
check_function_exists(strcasecmp HAVE_STRCASECMP)
check_function_exists(strchr HAVE_STRCHR)
check_function_exists(strup HAVE_STRUP)
check_function_exists(strerror HAVE_STRERROR)
check_include_files(strings.h HAVE_STRINGS_H)
check_include_files(string.h HAVE_STRING_H)
check_function_exists(strrchr HAVE_STRRCHR)
check_function_exists(strtol HAVE_STRTOL)
check_include_files(sys/stat.h HAVE_SYS_STAT_H)
check_include_files(sys/types.h HAVE_SYS_TYPES_H)
check_include_files(unistd.h HAVE_UNISTD_H)
check_include_files(windows.h HAVE_WINDOWS_H)
check_type_size(_Bool HAVE__BOOL)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/src/shared/config_cmake.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

#Build the application!
add_executable(gpx ${source_files})

#Installation.
include(GNUInstallDirs)
install(TARGETS gpx DESTINATION ${CMAKE_INSTALL_BINDIR})
