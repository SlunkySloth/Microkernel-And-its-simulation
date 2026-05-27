CC = gcc
AS = as

CFLAGS = -std=gnu99 -ffreestanding -O2 -Wall -Wextra -m32 -fno-pie
LDFLAGS = -ffreestanding -O2 -nostdlib -m32 -Wl,--build-id=none

OBJS = boot.o kernel.o

all: kernel.bin

boot.o: boot.s
	$(AS) --32 boot.s -o boot.o

kernel.o: kernel.c
	$(CC) -c kernel.c -o kernel.o $(CFLAGS)

kernel.bin: $(OBJS)
	$(CC) -T linker.ld -o kernel.bin $(OBJS) $(LDFLAGS) -lgcc

run: kernel.bin
	qemu-system-i386 -kernel kernel.bin

clean:
	rm -f *.o kernel.bin
