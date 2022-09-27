#CC	  = riscv64-unknown-linux-musl-gcc
CC = x86_64-linux-gnu-gcc
#CC = musl-gcc
PROF	= -DLINUX
NOCRYPT =
C_FLAGS = -Wall -pedantic -O3 $(PROF) $(NOCRYPT)
L_FLAGS = -O2 $(PROF) -lcrypt


O_FILES = admin.o banish.o bbs.o board.o command.o command2.o dbase.o editor.o \
	  mail.o message.o resolve.o user.o

ifeq ($(PREFIX),)
	PREFIX := ../build
endif

all: bbs

bbs: $(O_FILES)
	rm -f bbs ../lib/resolve
	$(CC)  $(O_FILES) $(L_FLAGS) -o bbs
	$(CC)  ../lib/resolve.c $(L_FLAGS) -o ../lib/resolve

.c.o: bbs.h
	$(CC) -c $(C_FLAGS) $<

clean:
	-rm -f *.o bbs ../lib/resolve

install:
	mkdir -p $(PREFIX)
	cp -a bbs $(PREFIX)/
	cp -a header.txt $(PREFIX)/
	cp -a ../lib/resolve $(PREFIX)/
	cp -a ../lib/bbs.config $(PREFIX)/
	cp -a ../lib/startup $(PREFIX)/
	cp -a ../lib/data $(PREFIX)/
	cp -a ../lib/user $(PREFIX)/


uninstall:
	rm -rf $(PREFIX)/*
