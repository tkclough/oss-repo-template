```Makefile
all: dynamic_block static_block

dynamic_block: program.o libblock.so
	gcc -L./ -o dynamic_block program.o -lblock

libblock.so: dynamic-block.o
	gcc -shared -o libblock.so dynamic-block.o

dynamic-block.o:
	gcc -o dynamic-block.o -c -fPIC source/block.c


static_block: program.o libblock.a
	gcc -o static_block program.o libblock.a

libblock.a: static-block.o
	ar rcs libblock.a static-block.o

static-block.o:
	gcc -c -o static-block.o -static source/block.c


program.o:
	gcc -c -o program.o program.c
```