#Copyright (C) 2007 L. Donnie Smith

include ../defs.mak

APP_NAME = wminput

SOURCES = main.c conf.c c_plugin.c uinput.c action_enum.c util.c
#kludge to make sure YACC/LEX sources are listed last, otherwise we get errors
#when building dependencies
LAST_SOURCES = parser.c lexer.c

WMINPUT_CONFIG_DIR = $(CWIID_CONFIG_DIR)/wminput
CFLAGS += -I../libcwiid \
	-DWMINPUT_CONFIG_DIR=\"$(WMINPUT_CONFIG_DIR)\" \
	-DCWIID_PLUGINS_DIR=\"$(CWIID_PLUGINS_DIR)\"

LDLIBS += -lcwiid -ldl
LDFLAGS += -L../libcwiid -rdynamic
INST_DIR = ${exec_prefix}/bin

YFLAGS += -d

ifdef PYTHON
	SOURCES += py_plugin.c
	CFLAGS += -I/usr/include/python2.5
	LDLIBS += -lpython2.5
endif

SOURCES += $(LAST_SOURCES)

include $(COMMON)/include/app.mak

all install clean distclean uninstall: make_plugins

install: install_configs

#DON'T UNINSTALL CONFIGS
#uninstall: uninstall_configs

make_plugins:
	$(MAKE) $(MAKECMDGOALS) -C plugins

install_configs:
	install -d $(WMINPUT_CONFIG_DIR)
	install configs/* $(WMINPUT_CONFIG_DIR)
	ln -sf acc_ptr $(WMINPUT_CONFIG_DIR)/default

#uninstall_configs:
#	rm -f $(WMINPUT_CONFIG_DIR)/default
#	for c in `ls configs`; do				\
#		rm -f $(WMINPUT_CONFIG_DIR)/$$c;	\
#	done
#	rmdir $(WMINPUT_CONFIG_DIR); true

action_enum.c: action_enum.awk action_enum.txt
	$(AWK) -f action_enum.awk action_enum.txt > action_enum.c

conf.o lexer.c: y.tab.h

y.tab.h: parser.c

clean: clean_gen

clean_gen:
	rm -f action_enum.c parser.c lexer.c y.tab.h

distclean: clean
	rm Makefile

.PHONY: all install clean distclean uninstall make_plugins clean_gen
