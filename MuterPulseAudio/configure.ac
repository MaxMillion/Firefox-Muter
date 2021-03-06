dnl Process this file with autoconf to produce a configure script.
# Prelude.
AC_PREREQ(2.59)
AC_INIT([MuterPulseAudio], [1.0], [http://yxl.github.com/Firefox-Muter/])
AC_CONFIG_SRCDIR(src/MuterPulseAudio.h)
AC_CONFIG_AUX_DIR([build-aux])
AC_CANONICAL_SYSTEM
AM_INIT_AUTOMAKE([-Wall -Werror])

# Checks for programss
AC_PROG_CXX
AC_PROG_LIBTOOL
LT_INIT

# Checks for libraries
dnl=======================================================================
dnl Check for Pulse Audio
dnl=======================================================================
PA_REQUIRED_VERSION=0.9.16

PKG_CHECK_MODULES(PULSEAUDIO,
        libpulse >= $PA_REQUIRED_VERSION 
        libpulse-mainloop-glib >= $PA_REQUIRED_VERSION,
        have_pulseaudio=yes,
        have_pulseaudio=no)
if test $have_pulseaudio = "no"; then
	AC_MSG_ERROR([PulseAudio dependencies have not been found!])
fi
AC_SUBST(PULSEAUDIO_CFLAGS)
AC_SUBST(PULSEAUDIO_LIBS)

# Checks for header files
AC_CHECK_HEADERS([fcntl.h]) 

# Checks for typedefs, structures
AC_HEADER_STDBOOL
AC_TYPE_SIZE_T 
AC_TYPE_UINT32_T

# Checks for library functions
AC_CHECK_FUNCS([strndup]) 

# Default compiler options
AC_ARG_ENABLE([debug],
              AS_HELP_STRING([--enable-debug], [enable debug [default=no]]),
              [enable_debug=$enableval],
              [enable_debug=no])
if test x$enable_debug = xyes; then
  CXXFLAGS="-g -O0 -Wall"
else 
  CXXFLAGS="-O2 -Wall"
fi
AC_ARG_ENABLE([m64],
              AS_HELP_STRING([--enable-m64], [generate 64-bit code [default=no]]),
              [enable_debug=$enableval],
              [enable_debug=no])
if test x$enable_m64 = xyes; then
  CXXFLAGS="$CXXFLAGS -m64"
else
  CXXFLAGS="$CXXFLAGS -m32"
fi

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES(Makefile src/Makefile)
AC_OUTPUT

