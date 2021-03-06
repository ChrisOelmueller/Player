#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.68])
AC_INIT([easyrpg-player],[0.1],[https://github.com/EasyRPG/Player/issues])

AM_INIT_AUTOMAKE([1.11 foreign -Wall -Werror -Wno-extra-portability])
AM_MAINTAINER_MODE([enable])
AM_SILENT_RULES([yes])

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADERS([config.h])


# Checks for programs.
AC_PROG_CXX
m4_ifdef([PKG_CHECK_MODULES],[],[AC_MSG_ERROR['pkg-config' is required but it doesn't seem to be installed on this system (PKG_CHECK_MODULES macro not found).]])

# Checks for libraries.
AC_ARG_WITH([readers],[AS_HELP_STRING([--with-readers=DIR],[Location of the EasyRPG 'readers' library])],[
	CXXFLAGS="$CXXFLAGS -I$withval/include"
	LDFLAGS="$LDFLAGS -L$withval/lib"
	AC_CHECK_LIB([readers],[ini_parse],[
		READERS_DIR=$withval
	],[AC_MSG_ERROR([EasyRPG 'readers' library does not have been found in the specified path.])])
])
PKG_CHECK_MODULES([PIXMAN],[pixman-1],[CXXFLAGS="$CXXFLAGS $PIXMAN_CFLAGS" LDFLAGS="$LDFLAGS $PIXMAN_LIBS"])
PKG_CHECK_MODULES([FREETYPE],[freetype2],[CXXFLAGS="$CXXFLAGS $FREETYPE_CFLAGS" LDFLAGS="$LDFLAGS $FREETYPE_LIBS"])
m4_ifdef([AM_PATH_SDL],[AM_PATH_SDL([1.2.0],[CXXFLAGS="$CXXFLAGS -DUSE_SDL $SDL_CFLAGS" LDFLAGS="$LDFLAGS $SDL_LIBS"])],[AC_MSG_ERROR['SDL' is required but it doesn't seem to be installed on this system (AM_PATH_SDL macro not found).]])
AC_CHECK_LIB([SDL_mixer],[Mix_OpenAudio],[CXXFLAGS="$CXXFLAGS -DHAVE_SDL_MIXER" LDFLAGS="$LDFLAGS -lSDL_mixer"],[AC_MSG_ERROR(['SDL_mixer' is required but it doesn't seem to be installed on this system.])])
AC_CHECK_LIB([png],[png_set_filler],[],[AC_MSG_ERROR(['libpng' is required but it doesn't seem to be installed on this system.])])
AC_CHECK_LIB([jpeg],[jpeg_mem_src],[],[AC_MSG_ERROR(['libjpeg' (with jpeg_mem_src) is required but it doesn't seem to be installed on this system.])])
AC_CHECK_LIB([z],[uncompress],[],[AC_MSG_ERROR(['zlib' is required but it doesn't seem to be installed on this system.])])
AC_CHECK_LIB([readers],[ini_parse],[],[AC_MSG_ERROR([EasyRPG 'readers' library is required but does not have been found. If you have already compiled it, use ./configure --with-readers=DIR to specify its location.])])

# Checks for header files.
AC_CHECK_HEADERS_ONCE([stddef.h stdint.h stdlib.h unistd.h wchar.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_INLINE
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_INT8_T
AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS_ONCE([floor memset putenv strerror])

AC_SUBST(READERS_DIR)

AC_CONFIG_FILES([Makefile
                 src/Makefile])

AC_OUTPUT
