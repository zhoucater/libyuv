lib_LTLIBRARIES = libyuv.la

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libyuv.pc

libyuvincludedir = $(includedir)
libyuvnobase_includedir = $(includedir)/libyuv

if WITH_MJPEG
mjpeg_SOURCES = mjpeg_decoder.cc
mjpeg_HDRS = ../include/libyuv/mjpeg_decoder.h
endif

if LIBYUV_POSIX
posix_SOURCES = row_posix.cc
endif

if LIBYUV_WINDOWS
windows_SOURCES = row_win.cc
endif

if ENABLE_NEON
neon_SOURCES = rotate_neon.cc row_neon.cc
endif

libyuvinclude_HEADERS = ../include/libyuv.h
libyuvnobase_include_HEADERS = ../include/libyuv/basic_types.h \
			       ../include/libyuv/compare.h \
			       ../include/libyuv/convert.h \
			       ../include/libyuv/convert_from.h \
			       ../include/libyuv/cpu_id.h \
			       ../include/libyuv/format_conversion.h \
			       ../include/libyuv/planar_functions.h \
			       ../include/libyuv/rotate.h \
			       ../include/libyuv/scale.h \
			       ../include/libyuv/version.h \
			       ../include/libyuv/video_common.h \
			       $(mjpeg_HDRS)

libyuv_la_SOURCES = compare.cc \
		    convert.cc \
		    convert_from.cc \
		    cpu_id.cc \
		    format_conversion.cc \
		    planar_functions.cc \
		    rotate.cc \
		    rotate_priv.h \
		    row.h \
		    row_common.cc \
		    scale.cc \
		    video_common.cc \
		    $(posix_SOURCES) \
		    $(windows_SOURCES) \
		    $(mjpeg_SOURCES) \
		    $(neon_SOURCES)

libyuv_la_CXXFLAGS = $(AM_LDFLAGS) -I$(top_srcdir)/include
libyuv_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(LIBYUV_VERSION_INFO)
libyuv_la_LIBADD = @LIBJPEG_LIBS@
