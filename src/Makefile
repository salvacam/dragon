#
# Copyright (C) 2007 Ludovic Jacomme (ludovic.jacomme@gmail.com)
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.
#
TARGET = gp2xdragon.gpe
SDL_CONFIG = $(GP2XDEV)/bin/sdl-config
OBJS = gp2x_psp.o \
psp_main.o \
psp_danzeff.o \
psp_fmgr.o \
psp_dragon.o \
psp_font.o \
psp_kbd.o \
psp_menu.o \
psp_menu_help.o \
psp_menu_kbd.o \
psp_menu_set.o \
psp_run.o \
psp_sdl.o \
global.o \
core/cart.o \
core/crc16.o \
core/deltados.o \
core/dragondos.o \
core/events.o \
core/filereq_cli.o \
core/fs_unix.o \
core/hexs19.o \
core/joystick.o \
core/keyboard.o \
core/m6809.o \
core/machine.o \
core/main_unix.o \
core/module.o \
core/pia.o \
core/rsdos.o \
core/sam.o \
core/snapshot.o \
core/sound_null.o \
core/sound_sdl.o \
core/tape.o \
core/ui_sdl.o \
core/vdg_bitmaps.o \
core/vdg.o \
core/vdisk.o \
core/vdrive.o \
core/video_sdl.o \
core/wd279x.o \
core/xroar.o \
core/keyboard_psp.o \
\
cpulcd.o

#PROFILE=-fprofile-generate
PROFILE=-fprofile-use

DEFAULT_CFLAGS = $(shell $(SDL_CONFIG) --cflags) 

MORE_CFLAGS = -DGP2X_MODE -static -I$(GP2XDEV)/include -I$(GP2XDEV)/include/SDL -DHAVE_CONFIG_H -I. -Iinclude \
           -DGP2X_MMU_HACK  -DPSP \
           -DNO_STDIO_REDIRECT  $(PROFILE)

CFLAGS = $(DEFAULT_CFLAGS) $(MORE_CFLAGS) -O2 \
    -funroll-loops -ffast-math -fomit-frame-pointer -fno-strength-reduce -finline-functions -fsigned-char
CXXFLAGS = $(DEFAULT_CFLAGS) $(MORE_CFLAGS) -O2 -fno-exceptions -fno-rtti \
    -funroll-loops -ffast-math -fomit-frame-pointer -fno-strength-reduce -finline-functions -fsigned-char

LIBS += -L$(GP2XDEV)/lib -lSDL_image -lSDL_fast -lpng -ljpeg -lz -lm -lpthread -lstdc++

.c.o:
	open2x-gcc $(CFLAGS) -c $< -o $@

.cpp.o:
	open2x-g++ $(CXXFLAGS) -c $< -o $@

$(TARGET): $(OBJS)
	open2x-gcc $(CFLAGS) $(OBJS) $(LIBS) -o $(TARGET) $(PROFILE)

install: $(TARGET)
	cp $< /media/usbdisk/game/dragon/

clean:
	rm -f $(OBJS) $(TARGET)

ctags: 
	ctags *[ch]
