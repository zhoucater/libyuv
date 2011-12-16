if WITH_TEST

TESTS = unit_test

noinst_PROGRAMS = $(TESTS)

unit_test_SOURCES = compare_test.cc \
		    cpu_test.cc \
		    planar_test.cc \
		    rotate_test.cc \
		    scale_test.cc \
		    unit_test.cc \
		    unit_test.h

unit_test_CXXFLAGS = $(AM_CXXFLAGS) @GTEST_CXXFLAGS@ -I$(top_srcdir)/include
unit_test_LDADD = @GTEST_LIBS@ $(top_builddir)/source/libyuv.la

else

TESTS =

endif

EXTRA_DIST = testdata/arm_v7.txt testdata/tegra3.txt
