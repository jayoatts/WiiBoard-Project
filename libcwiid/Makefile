#Copyright (C) 2006 L. Donnie Smith

include ../defs.mak

LIB_NAME = cwiid
MAJOR_VER = 1
MINOR_VER = 0
SOURCES = bluetooth.c command.c connect.c interface.c process.c state.c \
          thread.c util.c
LDLIBS += -lbluetooth -lpthread -lrt
LIB_INST_DIR = /usr/lib
INC_INST_DIR = ${prefix}/include

include $(COMMON)/include/lib.mak

$(SHARED_LIB): $(SO_NAME) $(LINK_NAME)

$(SO_NAME):
	ln -sf $(SHARED_LIB) $(SO_NAME)

$(LINK_NAME):
	ln -sf $(SO_NAME) $(LINK_NAME)

clean: remove_links

remove_links:
	rm -f $(SO_NAME) $(LINK_NAME)

distclean: clean
	rm Makefile

.PHONY: distclean clean make_links remove_links
