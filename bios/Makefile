include ../toolchain/*.mk

MMAP = mmap.x
ENDIANNESS = -EL
CFLAGS = -O0 -march=r3k -mno-abicalls -fno-pic -g3 -Wall -Wextra -Wno-main $(ENDIANNESS) \
	     -ffreestanding -nostdlib -nostartfiles
ASFLAGS = -march=r3k $(ENDIANNESS)
LDFLAGS = -ffreestanding -nostdlib -nostartfiles -T$(MMAP) -march=r3k $(ENDIANNESS)
ifeq ($(V), 1)
	LDFLAGS += -Wl,-verbose
endif

.DEFAULT: bios.bin
bios.bin: bios.elf
	$(OBJCOPY) -O binary $< $@

bios.elf: head.o shell.o uart16550.o tty.o string.o
	$(CC) $(LDFLAGS) -o$@ $^

.PHONY: clean
clean:
	rm -rf *.o *.elf *.bin

# vi: set shiftwidth=4 tabstop=4 noexpandtab:
# :indentSize=4:tabSize=4:noTabs=false:
