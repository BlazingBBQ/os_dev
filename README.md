# Simple OS for the i386 architecture

## To Do

### Main Goals
- [x] Boot + Hello World
- [x] Call C code from assembly
- [x] Framebuffer driver
- [x] Serial port driver
- [x] Segmentation
- [x] Interrupt handling
  + [x] Register interrupt handlers by interrupt number
  + [ ] Setup timer interrupt handler
- [x] Keyboard driver
- [x] Run GRUB modules
- [x] Enable paging
- [ ] Page frame allocation
- [ ] Create kernel heap
- [ ] Running C programs in User Mode
- [ ] Implement filesystem
- [ ] System calls
- [ ] Implement process scheduling

### Stretch Goals

- [ ] Simple shell
- [ ] File editor

### Side Quests:
- [ ] Better logging / printing
  + [x] newline characters
  + [ ] colors
  + [ ] log levels
- [ ] Util file:
  + [x] itoa
  + [x] str_reverse

## Development requirements

Install dependencies:

```
sudo apt install build-essential nasm genisoimage bochs bochs-sdl bochs-x
```

## Launch the os

### Make

```
Make run
```

### Manual

Generate loader.o: `nasm -f elf32 loader.s`

Link kernel.elf executable: `ld -T link.ld -melf_i386 loader.o -o kernel.elf`

Generate iso image:
```
genisoimage -R                              \
            -b boot/grub/stage2_eltorito    \
            -no-emul-boot                   \
            -boot-load-size 4               \
            -A os                           \
            -input-charset utf8             \
            -quiet                          \
            -boot-info-table                \
            -o os.iso                       \
            iso
```

Run Bochs: `bochs -f bochsrc.txt -q`
