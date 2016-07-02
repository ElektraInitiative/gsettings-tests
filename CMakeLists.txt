cmake_minimum_required (VERSION 3.0)
project(GSettingsTests VERSION 2.48.1 LANGUAGES C)
find_package (PkgConfig REQUIRED)
pkg_check_modules (GLIB glib-2.0>=2.42 REQUIRED)
pkg_check_modules (GMODULE gmodule-2.0>=2.42 REQUIRED)
pkg_check_modules (GIO gio-2.0>=2.42 REQUIRED)
include_directories (${GLIB_INCLUDE_DIRS})
add_executable (gsettings gsettings.c)
target_link_libraries (gsettings ${GLIB_LIBRARIES} ${GMODULE_LIBRARIES} ${GIO_LIBRARIES})
target_compile_definitions (gsettings PRIVATE SRCDIR="${CMAKE_CURRENT_SOURCE_DIR}")
file (
	COPY
		enums.xml.template
		org.gtk.schemasourcecheck.gschema.xml
		org.gtk.test.gschema.xml
		org.gtk.test.gschema.xml.orig
	DESTINATION
		${CMAKE_BINARY_DIR}
)
