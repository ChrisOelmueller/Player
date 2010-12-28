TARGET = EasyRPG
SOURCES = ../../../readers/src ../../src
CPPFILES = $(foreach dir,$(SOURCES), $(wildcard $(dir)/*.cpp))
BINFILES = $(foreach dir,$(DATA), $(wildcard $(dir)/*.*))
OBJS = $(addsuffix .o,$(BINFILES)) $(CPPFILES:.cpp=.o)
INCLUDES = ../../../readers/include ../../src

INCDIR = $(foreach dir,$(INCLUDES), -iquote $(CURDIR)/$(dir))
CFLAGS = -O2 -G0 -Wall -DPSP -DUSE_SDL
CXXFLAGS = $(CFLAGS) -fno-exceptions -fno-rtti
ASFLAGS = $(CFLAGS)

LIBDIR =
LDFLAGS = 

EXTRA_TARGETS = EBOOT.PBP
EXTRA_CLEAN = my-clean

PSP_EBOOT_TITLE = EasyRPG
PSP_EBOOT_ICON = "144x80.png"
PSP_EBOOT_PIC1 = "480x272.png"
PSP_DIR_NAME = easyrpg

PSPSDK=$(shell psp-config --pspsdk-path)
PSPBIN = $(PSPSDK)/../bin
CFLAGS += $(shell $(PSPBIN)/sdl-config --cflags)
LIBS += -lstdc++ -lSDL_ttf -lfreetype -lSDL_gfx -lSDL_mixer -lvorbisidec -lSDL_image -lsmpeg -lpng -ljpeg -lz -lm $(shell $(PSPBIN)/sdl-config --libs)
include $(PSPSDK)/lib/build.mak
