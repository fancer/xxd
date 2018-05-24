AC_PREREQ(2.69)
AC_INIT([xxd], [1.7], [jnweiger@informatik.uni-erlangen.de, fancer.lancer@gmail.com])

# Select UNIX system to build xxd
CFLAGS="$CFLAGS -DUNIX"

AM_INIT_AUTOMAKE([-Wall -Werror foreign])
AC_CONFIG_SRCDIR([src/])
AC_CONFIG_HEADER([src/config.h])

AC_PROG_CC

#Getting user and host info
username=$(whoami)
AC_MSG_CHECKING([user ID])
AC_MSG_RESULT([$username])

hostname=$(uname -n)
AC_MSG_CHECKING([host name])
AC_MSG_RESULT([$hostname])

timestamp=$(date)
AC_MSG_CHECKING([current timestamp])
AC_MSG_RESULT([$timestamp])

AC_DEFINE_UNQUOTED([RII_TIMESTAMP], "$username @ $hostname on $timestamp",
                   [Timestamp when ./configure was executed])

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdio.h fcntl.h unistd.h stdlib.h string.h ctype.h], [], [AC_MSG_FAILURE([Missing some header files.])])

# Checks for library functions.
AC_PROG_GCC_TRADITIONAL
AC_CHECK_FUNCS([fprintf fputs _flsbuf _filbuf fflush fclose fseek ferror rewind strtol strncmp strcpy open getc])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile])
AC_OUTPUT
