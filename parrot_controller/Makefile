##########################################################
# makefile for parrot-controller
##########################################################


# source PolySync environment if not already done, assumes x86_64 if set here
# usually, the environment has these set
PSYNC_HOME ?= /usr/local/polysync
OSPL_HOME ?= $(PSYNC_HOME)/utils/x86_64.linux

# target
TARGET	:= polysync-parrot-controller

# sources
SRCS    :=  src/ps_interface.c \
	    src/render.c \
	    src/grid.c \
	    src/gui.c \
	    src/parrot_controller.c \
	    src/waypoint.c \
	    src/vehicle_control.c

# object files, dep files
OBJS    := $(SRCS:.c=.o)
DEPS    := $(SRCS:.c=.dep)
XDEPS   := $(wildcard $(DEPS))

# get standard PolySync build resources
include $(PSYNC_HOME)/build_res.mk

# compiler
CC = gcc

# include GL EXT
CCFLAGS += -DGL_GLEXT_PROTOTYPES -DGLX_GLXEXT_PROTOTYPES

# includes
INCLUDE	+= -Iinclude

# libraries
LIBS	+= -lglut -lGLU -lGL -lX11 -lm -lpolysync_data_model

#
all: $(TARGET)

#
ifneq ($(XDEPS),)
include $(XDEPS)
endif

#
$(TARGET): $(OBJS)
	$(CC) $(LDFLAGS) $(INCLUDE) -o $@ $^ $(LIBS)

#
$(OBJS): %.o: %.c %.dep
	$(CC) $(CCFLAGS) $(INCLUDE) -o $@ -c $<

#
$(DEPS): %.dep: %.c Makefile
	$(CC) $(CCFLAGS) $(INCLUDE) -MM $< > $@

#
clean:
	-rm -f src/*.o
	-rm -f src/*.dep
	-rm -f $(TARGET)
	-rm -f ospl*
