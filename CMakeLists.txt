project(GPX)
cmake_minimum_required(VERSION 3.2.3) #Only version it's tested with.

#Where to find the source code.
set(source_files
	src/gpx/gpx-main.c
	src/gpx/gpx.c
	src/gpx/gpxresp.c
	src/gpx/vector.c
	src/gpx/winsio.c
	src/shared/machine_config.c
	src/shared/opt.c
	src/shared/s3g.c
	src/shared/s3g_stdio.c
	src/utils/machines.c
	src/utils/s3gdump.c
)
set(header_directories
	src
	src/gpx
	src/shared
)
include_directories(${CMAKE_CURRENT_BINARY_DIR} ${header_directories})

#Build the application!
add_executable(gpx ${source_files})

#Installation.
include(GNUInstallDirs)
install(TARGETS gpx DESTINATION ${CMAKE_INSTALL_BINDIR})
