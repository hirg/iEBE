# ===========================================================================
#  Makefile iS                                     Chun Shen Apr. 9, 2013
# ===========================================================================
##
##  Environments :	MAIN	= 	main sourcefile	
##
##  Usage : 	(g)make	[all]		compile the whole project		
##			install	make all and copy binary to $INSTPATH
##			clean		remove objectfiles in obj_$TYPE 
##			distclean	remove all objectsfiles and binaries
##  

CC := $(shell ../../crank/configure_compiler_C++.sh)
CFLAGS= -O3 -Wall

RM		=	rm -f
O               =       .o
LDFLAGS         =       $(CFLAGS)
SYSTEMFILES     =       $(SRCGNU)

# --------------- Files involved ------------------

ifeq "$(MAIN)" ""
MAIN		=	iS.e
endif

SRC		=	main.cpp arsenal.cpp emissionfunction.cpp \
			Table.cpp readindata.cpp ParameterReader.cpp

INC		= 	main.h arsenal.h emissionfunction.h \
                  Table.h readindata.h Stopwatch.h ParameterReader.h

# -------------------------------------------------

OBJDIR		=	obj
SRCFILES 	= 	$(SRC) $(INC) GNUmakefile
OBJECTS		=	$(addprefix $(OBJDIR)/, $(addsuffix $O, \
			$(basename $(SRC))))
TARGET		=	$(MAIN)
INSTPATH	=	../

# --------------- Pattern rules -------------------

$(OBJDIR)/%.o: %.cpp
	$(CC) $(CFLAGS) -c $< -o $@

%.cpp:
	if [ -f $@ ] ; then touch $@ ; else false ; fi

# -------------------------------------------------

.PHONY:		all mkobjdir clean distclean install

all:		mkobjdir $(TARGET)

help:
		@grep '^##' GNUmakefile

mkobjdir:	
		-@mkdir -p $(OBJDIR)

$(TARGET):	$(OBJECTS)	
		$(CC) $(OBJECTS) -o $(TARGET) $(LDFLAGS) 
#		strip $(TARGET)

clean:		
		-rm $(OBJECTS)

distclean:	
		-rm $(TARGET)
		-rm -r obj

install:	$(TARGET)
		cp $(TARGET) $(INSTPATH)

# --------------- Dependencies -------------------
./main.cpp: main.h Table.h readindata.h emissionfunction.h arsenal.h ParameterReader.h
./arsenal.cpp: arsenal.h
./emissionfunction.cpp: main.h readindata.h emissionfunction.h Stopwatch.h arsenal.h Table.h
./Table.cpp: Table.h arsenal.h
./readindata.cpp: main.h readindata.h arsenal.h Table.h ParameterReader.h
./ParameterReader.cpp: arsenal.h ParameterReader.h
