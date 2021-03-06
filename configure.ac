###############################################################################
# Copyright (c) 2011-2012 Los Alamos National Security, LLC.
#                         All rights reserved.
#
# This program was prepared by Los Alamos National Security, LLC at Los Alamos
# National Laboratory (LANL) under contract No. DE-AC52-06NA25396 with the U.S.
# Department of Energy (DOE). All rights in the program are reserved by the DOE
# and Los Alamos National Security, LLC. Permission is granted to the public to
# copy and use this software without charge, provided that this Notice and any
# statement of authorship are reproduced on all copies. Neither the U.S.
# Government nor LANS makes any warranty, express or implied, or assumes any
# liability or responsibility for the use of this software.
################################################################################

AC_PREREQ([2.60])

AC_INIT([supermagic], [1.3-dev], [samuel@lanl.gov])

dnl check if AM_SILENT_RULES are supported
dnl if so, build using AM_SILENT_RULES
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

dnl note: -Wall -Werror are automake options.  they are NOT compiler flags
AM_INIT_AUTOMAKE([-Wall -Werror foreign])

AM_CONFIG_HEADER([config.h])

dnl checks for programs.
dnl note that we are checking for mpicc first, the next check will verify CC
AC_PROG_CC([mpicc cc])

AM_PROG_CC_C_O
AC_PROG_CC_C99

AC_USE_SYSTEM_EXTENSIONS

AC_PROG_LIBTOOL
AC_CONFIG_MACRO_DIR([m4])

dnl check for adequate mpi support
AC_MSG_CHECKING([if $CC can compile MPI applications])
AC_LINK_IFELSE([
    AC_LANG_PROGRAM(
        [[#include <mpi.h>]],
        [[MPI_Finalize();]])],
    [AC_MSG_RESULT([yes])],
    [AC_MSG_RESULT([no])
     AC_MSG_ERROR([$CC cannot compile MPI applications. cannot continue.])]
)

dnl checks for libraries.
SMGC_CELL

dnl checks for header files.
AC_CHECK_HEADERS([\
inttypes.h limits.h stdint.h stdlib.h string.h unistd.h \
getopt.h time.h string.h fcntl.h limits.h arpa/inet.h netdb.h \
sys/time.h stdint.h stdio.h errno.h stdbool.h signal.h])

dnl checks for typedefs, structures, and compiler characteristics.
AC_TYPE_PID_T
AC_TYPE_SIZE_T

dnl checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([memset strerror strtoul])

AC_CONFIG_FILES([Makefile
                 cell/Makefile
                 cell/ppu/Makefile])

AC_OUTPUT

dnl let the user know the configuration

cat << EOF

supermagic configuration
########################

CC      : $CC
CFLAGS  : $CFLAGS
LDFLAGS : $LDFLAGS
LIBS    : $LIBS
CPPFLAGS: $CPPFLAGS
CPP     : $CPP

EOF
