OBJS=moptrace.o 
INCL=-I../ -I../common
LIBS=../common/libcommon.a

all: moptrace

moptrace: ${OBJS} version.o $(LIBS)
	cc -o moptrace version.o ${OBJS} ${LIBS}

install: all
	install -m 755 moptrace $(DESTDIR)$(BINDIR)
	install -m 644 moptrace.1 $(DESTDIR)$(MANDIR)/man1

.c.o: .c
	cc -c $(CFLAGS) ${INCL} $<
	
clean:
	rm -f *.o *~ moptrace VERSION version.*
	
version.o: version.c
version.c version.h: 
	ln -sf ../common/VERSION VERSION
	rm -f version.c ; sed 's/.*/char version[] = "&";/' VERSION > version.c
	set `sed 's/\([0-9]*\)\.\([0-9]*\).*/\1 \2/' VERSION` ; \
		{ echo '#define VERSION_MAJOR' $$1 ; \
		  echo '#define VERSION_MINOR' $$2 ; } > version.h
 
