include $(top_srcdir)/Makefile.am.in

bin_PROGRAMS = ndctl

ndctl_SOURCES = ndctl.c \
		bus.c \
		create-nfit.c \
		namespace.c \
		check.c \
		region.c \
		dimm.c \
		 ../util/log.c \
		list.c \
		../util/json.c \
		util/json-smart.c \
		util/json-firmware.c \
		inject-error.c \
		inject-smart.c \
		monitor.c

if ENABLE_DESTRUCTIVE
ndctl_SOURCES += ../test/blk_namespaces.c \
		 ../test/pmem_namespaces.c
ndctl_SOURCES += bat.c
endif

ndctl_LDADD =\
	lib/libndctl.la \
	../daxctl/lib/libdaxctl.la \
	../libutil.a \
	$(UUID_LIBS) \
	$(KMOD_LIBS) \
	$(JSON_LIBS)

if ENABLE_TEST
ndctl_SOURCES += ../test/libndctl.c \
		 ../test/dsm-fail.c \
		 ../util/sysfs.c \
		 ../test/dpa-alloc.c \
		 ../test/parent-uuid.c \
		 ../test/multi-pmem.c \
		 ../test/core.c \
		 test.c
endif

monitor_config_file = monitor.conf
monitor_configdir = $(sysconfdir)/ndctl/
monitor_config_DATA = $(monitor_config_file)
EXTRA_DIST += $(monitor_config_file)

if ENABLE_SYSTEMD_UNITS
systemd_unit_DATA = ndctl-monitor.service
endif
