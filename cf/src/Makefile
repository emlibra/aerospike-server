# Citrusleaf Foundation
# Makefile

DEPTH = ../..
include $(DEPTH)/make_in/Makefile.in

ifeq ($(USE_EE),1)
  include $(EEREPO)/cf/make_in/Makefile.vars
endif

HEADERS += arenax.h bits.h cf_mutex.h cf_str.h cf_thread.h compare.h daemon.h
HEADERS += dns.h dynbuf.h enhanced_alloc.h epoll_queue.h hist.h hist_track.h
HEADERS += linear_hist.h log.h msg.h msgpack_in.h node.h rchash.h shash.h
HEADERS += socket.h tls.h vmapx.h xmem.h

# Temporary until all #include "fault.h" are replaced with #include "log.h".
HEADERS += fault.h

SOURCES += alloc.c arenax.c cf_mutex.c cf_str.c cf_thread.c daemon.c dns.c
SOURCES += dynbuf.c epoll_queue.c hardware.c hist.c hist_track.c linear_hist.c
SOURCES += log.c msg.c msgpack_in.c node.c rchash.c shash.c socket.c vmapx.c

ifneq ($(USE_EE),1)
  SOURCES += arenax_ce.c socket_ce.c tls_ce.c
endif

LIBRARY = $(LIBRARY_DIR)/libcf.a

INCLUDES += $(INCLUDE_DIR:%=-I%) -I$(COMMON)/src/include

OBJECTS = $(SOURCES:%.c=$(OBJECT_DIR)/%.o)
DEPENDENCIES = $(OBJECTS:%.o=%.d)

.PHONY: all
all: $(LIBRARY)

.PHONY: clean
clean:
	$(RM) $(OBJECTS) $(LIBRARY)
	$(RM) $(DEPENDENCIES)

$(LIBRARY): $(OBJECTS)
	$(AR) rs $(LIBRARY) $(OBJECTS)

include $(DEPTH)/make_in/Makefile.targets
