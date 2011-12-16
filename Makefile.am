lib_LTLIBRARIES = libyuv.la

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libyuv.pc

libyuvincludedir = $(includedir)
libyuvnobase_includedir = $(includedir)/libyuv

if WITH_MJPEG
mjpeg_HDRS = include/libyuv/mjpeg_decoder.h
mjpeg_SOURCES = source/convert_jpeg.cc \
		source/mjpeg_decoder.cc \
		source/mjpeg_validate.cc
endif

if LIBYUV_POSIX
posix_SOURCES = source/compare_posix.cc \
		source/row_posix.cc
endif

if LIBYUV_WINDOWS
windows_SOURCES = source/compare_win.cc \
		  source/row_win.cc
endif

if ENABLE_MIPS
mips_SOURCES = source/memcpy_mips.S \
	       source/rotate_mips.cc \
	       source/row_mips.cc \
	       source/scale_mips.cc
endif

if ENABLE_X86
x86_SOURCES = source/row_x86.asm \
	      source/x86inc.asm
endif

if ENABLE_NEON
neon_SOURCES = source/compare_neon.cc \
	       source/rotate_neon.cc \
	       source/row_neon.cc \
	       source/scale_argb_neon.cc \
	       source/scale_neon.cc
endif

libyuvinclude_HEADERS = include/libyuv.h
libyuvnobase_include_HEADERS = include/libyuv/basic_types.h \
			       include/libyuv/compare.h \
			       include/libyuv/convert.h \
			       include/libyuv/convert_argb.h \
			       include/libyuv/convert_from.h \
			       include/libyuv/convert_from_argb.h \
			       include/libyuv/cpu_id.h \
			       include/libyuv/format_conversion.h \
			       include/libyuv/planar_functions.h \
			       include/libyuv/rotate.h \
			       include/libyuv/rotate_argb.h \
			       include/libyuv/row.h \
			       include/libyuv/scale.h \
			       include/libyuv/scale_argb.h \
			       include/libyuv/version.h \
			       include/libyuv/video_common.h \
			       $(mjpeg_HDRS)

libyuv_la_SOURCES = source/compare.cc \
		    source/compare_common.cc \
		    source/convert.cc \
		    source/convert_argb.cc \
		    source/convert_from.cc \
		    source/convert_from_argb.cc \
		    source/convert_to_argb.cc \
		    source/convert_to_i420.cc \
		    source/cpu_id.cc \
		    source/format_conversion.cc \
		    source/planar_functions.cc \
		    source/rotate.cc \
		    source/rotate_argb.cc \
		    source/row_any.cc \
		    source/row_common.cc \
		    source/scale.cc \
		    source/scale_argb.cc \
		    source/scale_common.cc \
		    source/video_common.cc \
		    $(mjpeg_SOURCES) \
		    $(posix_SOURCES) \
		    $(windows_SOURCES) \
		    $(mips_SOURCES) \
		    $(neon_SOURCES) \
		    $(x86_SOURCES)

libyuv_la_CXXFLAGS = $(AM_LDFLAGS) -I$(top_srcdir)/include -I$(top_srcdir)
libyuv_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(LIBYUV_VERSION_INFO)
libyuv_la_LIBADD = @LIBJPEG_LIBS@

EXTRA_DIST = AUTHORS Android.mk DEPS LICENSE PATENTS README.chromium codereview.settings libyuv.gyp libyuv_test.gyp tools/valgrind-libyuv/* unit_test/testdata/arm_v7.txt unit_test/testdata/tegra3.txt util/compare.cc

if WITH_TEST

TESTS = unittest

noinst_PROGRAMS = $(TESTS)

unittest_SOURCES = unit_test/basictypes_test.cc \
		   unit_test/compare_test.cc \
		   unit_test/convert_test.cc \
		   unit_test/cpu_test.cc \
		   unit_test/math_test.cc \
		   unit_test/planar_test.cc \
		   unit_test/rotate_argb_test.cc \
		   unit_test/rotate_test.cc \
		   unit_test/scale_argb_test.cc \
		   unit_test/scale_test.cc \
		   unit_test/unit_test.cc \
		   unit_test/unit_test.h \
		   unit_test/version_test.cc \
		   unit_test/video_common_test.cc

unittest_CXXFLAGS = $(AM_CXXFLAGS) @GTEST_CXXFLAGS@ -I$(top_srcdir)/include -I$(top_srcdir)
unittest_LDADD = @GTEST_LIBS@ $(top_builddir)/libyuv.la

endif
