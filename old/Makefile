PLATNAME := $(shell uname)

OBJS	=	clexer.o \
		cgrammar.o


TARGET	=	tester

CARGS	=	-Wall
DEBUG	=	-g -DTRACE
HEADERS	=	$(OBJS:.o=.h)

ifeq ($(PLATNAME), Linux)
	LIBS	=	-ll -ly
else ifeq ($(PLATNAME), MSYS_NT-6.1)
	LIBS	=	-L/c/MinGW/msys/1.0/lib -lfl -ly
endif

.c.o:
	gcc $(CARGS) $(DEBUG) -c $< -o $@

all: $(TARGET)

$(TARGET): $(OBJS1) $(OBJS)
	gcc $(CARGS) $(DEBUG) $(OBJS1) $(OBJS) -o $(TARGET) $(LIBS)

cgrammar.c cgrammar.h: cgrammar.bison
	bison -vdo cgrammar.c cgrammar.bison

clexer.c: clexer.flex cgrammar.h
	flex -o clexer.c clexer.flex

cgrammar.o: cgrammar.c
clexer.o: clexer.c cgrammar.h

clean:
	-rm -f clexer.c cgrammar.c cgrammar.h cgrammar.output $(OBJS1) $(OBJS) $(TARGET)

