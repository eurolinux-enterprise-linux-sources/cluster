include ../../make/defines.mk

TARGET= gfs_controld

SBINDIRT=$(TARGET)

all: depends ${TARGET}

include $(OBJDIR)/make/cobj.mk
include $(OBJDIR)/make/clean.mk
include $(OBJDIR)/make/install.mk
include $(OBJDIR)/make/uninstall.mk

OBJS= 	main.o \
	crc.o \
	config.o \
	cpg-new.o \
	cpg-old.o \
	group.o \
	util.o \
	plock.o \
	logging.o \
	member_cman.o

CFLAGS += -I${ccsincdir} -I${cmanincdir} -I${logtincdir} -I${dlmcontrolincdir}
CFLAGS += -I${corosyncincdir} -I${openaisincdir} -I${fencedincdir}
CFLAGS += -I${KERNEL_SRC}/include/
CFLAGS += -I$(S)/../libgfscontrol
CFLAGS += -I$(S)/../lib/ -I$(S)/../include/
CFLAGS += -I${incdir}

LDFLAGS += -L${ccslibdir} -L${cmanlibdir} -lccs -lcman
LDFLAGS += -L${fencedlibdir} -lfenced
LDFLAGS += -L${dlmcontrollibdir} -ldlmcontrol
LDFLAGS += -L${logtlibdir} -llogthread
LDFLAGS += -L${corosynclibdir} -lcpg -lpthread
LDFLAGS += -L${openaislibdir} -lSaCkpt
LDFLAGS += -L../lib -lgroup
LDFLAGS += -L${libdir}

LDDEPS += ../lib/libgroup.a

gfs_controld: ${OBJS} ${LDDEPS}
	$(CC) -o $@ $^ $(LDFLAGS)

depends:
	$(MAKE) -C ../lib all

clean: generalclean

-include $(OBJS:.o=.d)
