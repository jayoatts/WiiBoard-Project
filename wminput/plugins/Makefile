#Copyright (C) 2007 L. Donnie Smith

include ../../defs.mak

PLUGINS = ir_ptr acc nunchuk_acc

all install clean distclean uninstall: TARGET += $(MAKECMDGOALS)

all install clean distclean uninstall: $(PLUGINS)

$(PLUGINS):
	$(MAKE) $(TARGET) -C $@

distclean: clean
	rm Makefile

.PHONY: all install clean distclean uninstall $(PLUGINS)
