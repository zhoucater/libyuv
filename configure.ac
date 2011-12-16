AC_INIT([libyuv], [0], [http://groups.google.com/group/discuss-libyuv], [libyuv], [http://code.google.com/p/libyuv/])

AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([dist-bzip2 no-dist-gzip tar-ustar foreign])

AC_SUBST(LIBYUV_VERSION_INFO, [0:0:0])

AC_PROG_CXX
AC_PROG_LIBTOOL
AC_PROG_INSTALL

AC_LANG_CPLUSPLUS

AC_ARG_WITH([mjpeg],
	    AC_HELP_STRING([--with-mjpeg],[enable Motion JPEG decoder.]),
	    [with_mjpeg="$withval"],[with_mjpeg="no"]
	    )

if test "$with_mjpeg" = "yes" ; then
	AC_MSG_WARN([Motion JPEG decoder is enabled])
	AC_CHECK_HEADERS(
			 [jpeglib.h],
			 [],
			 [AC_MSG_ERROR([jpeglib.h header not found])],
			 [AC_INCLUDES_DEFAULT]
			 )
	AC_CHECK_LIB(
		     [jpeg],
		     [jpeg_read_header],
		     [
		      CXXFLAGS="$CXXFLAGS -DHAVE_JPEG"
		      LIBJPEG_LIBS="-ljpeg"
		      AC_SUBST([LIBJPEG_LIBS])
		      ],
		     [AC_MSG_ERROR([libjpeg or libjpeg-turbo library not found])],
		     []
		     )

else
	AC_MSG_WARN([Motion JPEG decoder is disabled])
fi


AC_ARG_WITH([test],
	    AC_HELP_STRING([--with-test],[enable test suite.]),
	    [with_test="$withval"],[with_test="no"]
	    )

if test "$with_test" = "yes" ; then
	AC_MSG_WARN([Test suite is enabled])
	AC_CHECK_HEADERS(
			 [gtest/gtest.h],
			 [],
			 [AC_MSG_ERROR([gtest not found])],
			 []
			 )
	AC_PATH_PROG([GTEST_CONFIG], gtest-config, [no])
	if test "$GTEST_CONFIG" = "no" ; then
		AC_MSG_ERROR([gtest-config was not found])
	fi
	GTEST_CXXFLAGS=`$GTEST_CONFIG --cxxflags`
	GTEST_LIBS=`$GTEST_CONFIG --libs`
	AC_SUBST([GTEST_CXXFLAGS])
	AC_SUBST([GTEST_LIBS])
else
	AC_MSG_WARN([Test suite is disabled])
fi

case "$target_os" in
	linux*)
		posix="yes"
		;;
	darwin*)
		posix="yes"
		;;
	mingw*)
#		windows="yes"
		posix="yes"
		LDFLAGS="$LDFLAGS -no-undefined --enable-runtime-pseudo-reloc -avoid-version"
		;;
	*)
		AC_MSG_ERROR([No support for this target ($target) yet])
		;;
esac

case "$target_cpu" in
	arm*)
		AC_ARG_ENABLE(neon,
			      [  --enable-neon           enable ARM NEON support],
			      [
			       AC_MSG_CHECKING(for NEON in current arch/CFLAGS)
			       AC_LINK_IFELSE([
					       AC_LANG_PROGRAM(
							       [[
								#include <arm_neon.h>
								int32x4_t testfunc(int16_t *a, int16_t *b)
								{
									return vmull_s16(vld1_s16(a), vld1_s16(b));
								}
								]]
							       )
					       ],
					       [has_neon=yes],
					       [has_neon=no]
					      )
			       AC_MSG_RESULT($has_neon)
			      ]
			     )
		;;
	*)
		has_neon="no"
		;;
esac

AC_CONFIG_FILES([
Makefile
source/libyuv.pc
source/Makefile
unit_test/Makefile
])

AM_CONDITIONAL(LIBYUV_POSIX, test "$posix" = "yes")
AM_CONDITIONAL(LIBYUV_WINDOWS, test "$windows" = "yes")

AM_CONDITIONAL(WITH_MJPEG, test "$with_mjpeg" = "yes")
AM_CONDITIONAL(WITH_TEST, test "$with_test" = "yes")
AM_CONDITIONAL(ENABLE_NEON, test "$has_neon" = "yes")

AC_OUTPUT

AC_MSG_RESULT([
------------------------------------------------------------------------
  $PACKAGE $VERSION configuration.

    Compiler support:

      Target CPU: ................... ${target_cpu}
             Has NEON? .............. ${has_neon}
      Target OS: .................... ${target_os}
             Is POSIX? .............. ${posix}

    General configuration:

      Enable Motion JPEG: ............ ${with_mjpeg}
      Enable test suite: . ........... ${with_test}

------------------------------------------------------------------------
])
