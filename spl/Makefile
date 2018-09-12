subdir-m += spl
subdir-m += splat

INSTALL_MOD_DIR ?= extra

SPL_MODULE_CFLAGS  = -I/work/git/spl/include
SPL_MODULE_CFLAGS += -include /work/git/spl/spl_config.h
export SPL_MODULE_CFLAGS

modules:
	$(MAKE) -C ../linux-stable SUBDIRS=`pwd`  CONFIG_SPL=m $@

clean:
	@# Only cleanup the kernel build directories when CONFIG_KERNEL
	@# is defined.  This indicates that kernel modules should be built.
#	$(MAKE) -C ../linux-stable SUBDIRS=`pwd`  $@

	if [ -f NONE ]; then $(RM) NONE; fi
	if [ -f Module.markers ]; then $(RM) Module.markers; fi

modules_install:
	@# Install the kernel modules
	$(MAKE) -C ../linux-stable SUBDIRS=`pwd` $@ \
		INSTALL_MOD_PATH=$(DESTDIR)$(INSTALL_MOD_PATH) \
		INSTALL_MOD_DIR=$(INSTALL_MOD_DIR) \
		KERNELRELEASE=4.14.69+
	@# Remove extraneous build products when packaging
	kmoddir=$(DESTDIR)$(INSTALL_MOD_PATH)/lib/modules/4.14.69+; \
	if [ -n "$(DESTDIR)" ]; then \
		find $$kmoddir -name 'modules.*' | xargs $(RM); \
	fi
	sysmap=$(DESTDIR)$(INSTALL_MOD_PATH)/boot/System.map-4.14.69+; \
	if [ -f $$sysmap ]; then \
		depmod -ae -F $$sysmap 4.14.69+; \
	fi

modules_uninstall:
	@# Uninstall the kernel modules
	kmoddir=$(DESTDIR)$(INSTALL_MOD_PATH)/lib/modules/4.14.69+
	list='$(subdir-m)'; for subdir in $$list; do \
		$(RM) -R $$kmoddir/$(INSTALL_MOD_DIR)/$$subdir; \
	done

distdir:
	list='$(subdir-m)'; for subdir in $$list; do \
		(find ../module/$$subdir -name '*.c' -o -name '*.h' |\
		 xargs /bin/cp -t $$distdir/$$subdir); \
	done

distclean maintainer-clean: clean
install: modules_install
uninstall: modules_uninstall
all: modules
check:
