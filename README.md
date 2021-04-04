# ASM
Simple Kernal using C

## Run os
You can use VirtualBox to open the ISO file after configring it.
ISO file is in the repository.

Feel Free to make pull requests and issues.

Build the boot.asm into an object file:


    $ nasm -f elf32 boot.asm -o boot.o

Build the kernel.c into an object file:


    $ gcc -m32 -c kernel.c -o kernel.o

Link both object files and create the final executable program (that is, your kernel):


    $ ld -m elf_i386 -T linker.ld -o kernel boot.o kernel.o

Now, you should have a compiled file in the same working directory labeled kernel:


    $ ls
    boot.asm  boot.o  grub.cfg  kernel  kernel.c  kernel.o
 ↪linker.ld

This file is your kernel. You'll be booting into that kernel shortly.

Building a Bootable ISO Image
Create a staging environment with the following directory path (from your current working directory path):


    $ mkdir -p iso/boot/grub

Let's double-check that the kernel is a multiboot file type (no output is expected with a return code of 0):


    $ grub-file --is-x86-multiboot kernel

Now, copy the kernel into your iso/boot directory:


    $ cp kernel iso/boot/

And, copy your grub.cfg into the iso/boot/grub directory:


    $ cp grub.cfg iso/boot/grub/

Make the final ISO image pointing to your iso subdirectory in your current working directory path:

    $ grub-mkrescue -o my-kernel.iso iso/
    xorriso 1.4.8 : RockRidge filesystem manipulator,
    ↪libburnia project.

    Drive current: -outdev 'stdio:my-kernel.iso'
    Media current: stdio file, overwriteable
    Media status : is blank
    Media summary: 0 sessions, 0 data blocks, 0 data, 10.3g free
    Added to ISO image: directory '/'='/tmp/grub.fqt0G4'
    xorriso : UPDATE : 284 files added in 1 seconds
    Added to ISO image: directory
    ↪'/'='/home/petros/devel/misc/kernel/iso'
    xorriso : UPDATE : 288 files added in 1 seconds
    xorriso : NOTE : Copying to System Area: 512 bytes from file
    ↪'/usr/lib/grub/i386-pc/boot_hybrid.img'
    ISO image produced: 2453 sectors
    Written to medium : 2453 sectors at LBA 0
    Writing to 'stdio:my-kernel.iso' completed successfully.
