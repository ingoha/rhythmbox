NULL =

plugindir = $(PLUGINDIR)/mtpdevice
plugindatadir = $(PLUGINDATADIR)/mtpdevice
plugin_LTLIBRARIES = libmtpdevice.la

libmtpdevice_la_SOURCES = \
	mtpdevice-resources.c \
	rb-mtp-plugin.c	\
	rb-mtp-gst.c \
	rb-mtp-gst.h \
	rb-mtp-gst-src.c \
	rb-mtp-gst-sink.c \
	rb-mtp-source.c	\
	rb-mtp-source.h \
	rb-mtp-thread.c \
	rb-mtp-thread.h
	
libmtpdevice_la_LDFLAGS = $(PLUGIN_LIBTOOL_FLAGS)
libmtpdevice_la_LIBTOOLFLAGS = --tag=disable-static
libmtpdevice_la_LIBADD = 				\
	$(top_builddir)/shell/librhythmbox-core.la	\
	$(GUDEV_LIBS)					\
	$(HAL_LIBS)					\
	$(MTP_LIBS)

AM_CPPFLAGS = 						\
        -DGNOMELOCALEDIR=\""$(datadir)/locale"\"        \
	-DG_LOG_DOMAIN=\"Rhythmbox\"		 	\
	-I$(top_srcdir) 				\
	-I$(top_srcdir)/backends			\
	-I$(top_srcdir)/lib                        	\
	-I$(top_srcdir)/lib/libmediaplayerid          	\
	-I$(top_srcdir)/metadata                       	\
	-I$(top_srcdir)/rhythmdb                       	\
	-I$(top_srcdir)/widgets                    	\
	-I$(top_srcdir)/sources                    	\
	-I$(top_srcdir)/sources/sync                   	\
	-I$(top_srcdir)/podcast                    	\
	-I$(top_srcdir)/plugins                    	\
	-I$(top_srcdir)/shell				\
	-DPIXMAP_DIR=\""$(datadir)/pixmaps"\"		\
	-DSHARE_DIR=\"$(pkgdatadir)\"                   \
	-DDATADIR=\""$(datadir)"\"			\
	$(RHYTHMBOX_CFLAGS)				\
	$(GUDEV_CFLAGS)					\
	$(HAL_CFLAGS)					\
	$(MTP_CFLAGS)

plugin_in_files = mtpdevice.plugin.in

%.plugin: %.plugin.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

plugin_DATA = $(plugin_in_files:.plugin.in=.plugin)

PLUGIN_RESOURCES = 					\
	mtp-info.ui					\
	mtp-toolbar.ui

plugin_resource_deps = $(shell $(GLIB_COMPILE_RESOURCES) --generate-dependencies --sourcedir $(srcdir) $(srcdir)/mtpdevice.gresource.xml)
mtpdevice-resources.c: $(plugin_resource_deps) $(srcdir)/mtpdevice.gresource.xml
	$(AM_V_GEN) $(GLIB_COMPILE_RESOURCES)		\
		--target="$@"				\
		--sourcedir="$(srcdir)"			\
		--sourcedir="$(builddir)"		\
		--generate-source "$(srcdir)/mtpdevice.gresource.xml"

BUILT_SOURCES = $(plugin_DATA) mtpdevice-resources.c

EXTRA_DIST = $(plugin_in_files) $(PLUGIN_RESOURCES) mtpdevice.gresource.xml

CLEANFILES = $(BUILT_SOURCES)
DISTCLEANFILES = $(BUILT_SOURCES)
