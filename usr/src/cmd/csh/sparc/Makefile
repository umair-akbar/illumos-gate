# Copyright (c) 1992, 2010, Oracle and/or its affiliates. All rights reserved.

#	Copyright (c) 1983, 1984, 1985, 1986, 1987, 1988, 1989 AT&T
#	  All Rights Reserved

# Copyright (c) 1980 Regents of the University of California.
# All rights reserved.  The Berkeley Software License Agreement
# specifies the terms and conditions for redistribution.

#
# C Shell with process control; VM/UNIX VAX Makefile
# Bill Joy UC Berkeley; Jim Kulp IIASA, Austria
#

CSH_PROG =	csh
PROG =		$(CSH_PROG)

include ../../Makefile.cmd

MBCHAR	= -DMBCHAR	# Define this line to include multibyte input support
DEFS	=  -DVFORK -DFILEC -DBSD_COMP -DFIVE	# No TELL when MBCHAR
CPPFLAGS= -I. $(DEFS) $(MBCHAR) $(CPPFLAGS.master)
CPPFLAGS +=	-I../../sh
CPPFLAGS += -D_FILE_OFFSET_BITS=64
CERRWARN += -_gcc=-Wno-implicit-function-declaration
CERRWARN += $(CNOWARN_UNINIT)
CERRWARN += -_gcc=-Wno-parentheses
CERRWARN += -_gcc=-Wno-implicit-int
CERRWARN += -_gcc=-Wno-unused-function
CERRWARN += -_gcc=-Wno-unused-variable
CERRWARN += -_gcc=-Wno-clobbered
CERRWARN += -_gcc=-Wno-unused-label
CERRWARN += -_gcc=-Wno-extra

LDLIBS += -lcurses

MAPFILES =	../mapfile-intf $(MAPFILE.NGB)
LDFLAGS +=	$(MAPFILES:%=-Wl,-M%)

PFOBJS = sh_policy.o

HDDEP = sh.o sh.dir.o sh.dol.o sh.err.o sh.exec.o sh.exp.o sh.file.o \
	sh.func.o sh.glob.o sh.hist.o sh.init.o sh.lex.o sh.misc.o \
	sh.parse.o sh.proc.o sh.sem.o sh.set.o sh.time.o

COMMONOBJS=	printf.o sh.char.o sh.dir.o sh.dol.o sh.err.o \
	sh.exec.o sh.exp.o sh.file.o sh.func.o sh.glob.o sh.hist.o sh.init.o \
	sh.lex.o sh.misc.o sh.parse.o sh.print.o sh.proc.o sh.sem.o sh.set.o \
	sh.time.o sh.tchar.o sh.tconst.o sh.o \
        wait3.o

LOCALOBJS= signal.o

COMMONSRCS=	$(COMMONOBJS:%.o=../%.c)

.KEEP_STATE:

.PARALLEL: $(COMMONOBJS) $(LOCALOBJS)

all: $(PROG)

# build rule for common source above
%.o:	../%.c
	$(COMPILE.c) $<
	$(POST_PROCESS_O)

%.o:	../../sh/%.c
	$(COMPILE.c) $<
	$(POST_PROCESS_O)

$(CSH_PROG): $(COMMONOBJS) $(LOCALOBJS) $(MAPFILES)
	$(LINK.c) $(COMMONOBJS) $(LOCALOBJS) -o $@ $(LDLIBS)
	$(POST_PROCESS)

$(HDDEP): ../sh.tconst.h

install: all $(ROOTBINPROG)  $(ROOTPROG)

clean:
	$(RM) $(LOCALOBJS) $(COMMONOBJS)

clobber:	clean
	$(RM)  $(PROG)
