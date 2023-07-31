## understanding linux 0.11 internal

```
    The current Linux kernel runs into the millions of lines of code, add to that the other critical parts of a modern operating system (the compiler, assembler and system libraries) and your code base becomes unimaginable. Further still, add a University level operating systems course (or four), some good reference manuals, two or three years of C experience and, just maybe, you might be able to figure out where to start looking to make sense of it all. - Ian Wienand

```


### Booting 
- everything is start from 0xFFFF0 => boots/bootsect.s  
    - it start with assembly/hardware language not c language cause ram and cpu even didn't start.  
    - As a general rule, the Linux kernel is installed in RAM starting from the physical address 0x00100000  
    - what it means? One way to implement NOT is to use XOR with one operand being all ones (FFFF FFFF FFFF FFFFhex).  
    - Page frame 0 is used by BIOS to store the system hardware configuration
detected during the Power-On Self-Test (POST); the BIOS of many laptops,
moreover, writes data on this page frame even after the system is initialized.  
    - For example, registers that are 32 bits wide can hold addresses in a register range from 0x00000000 to 0xFFFFFFF 
    - Physical addresses ranging from 0x000a0000 to 0x000fffff are usually reserved to BIOS routines and to map the internal memory of ISA graphics cards. This area
is the well-known hole from 640 KB to 1 MB in all IBM-compatible PCs

Example of BIOS-provided physical addresses map
|Start |End |Type |
|------|----|-----|
| 0x00000000 | 0x0009ffff |Usable    |  
| 0x000f0000 | 0x000fffff |Reserved  |
| 0x00100000 | 0x07feffff |Usable    |
| 0x07ff0000 | 0x07ff2fff |ACPI data |
| 0x07ff3000 | 0x07ffffff |ACPI NVS  |
| 0xffff0000 | 0xffffffff |Reserved  |

   - memory from 0xF0000-0xFFFFF is reserved for the system BIOS. Also, since system BIOS has become more complex over the years, many platforms also use 0xE0000-0xEFFFF for system BIOS
   - When an Intel architecture boot-strap processor (BSP) powers on, the first
address fetched and executed is at physical address 0xFFFFFFF0, also known as the reset vector. This accesses the ROM or flash device at the top of the ROM: 0x10. The boot loader must always contain a jump to the initialization code in these top 16 bytes.
    - FFFF0H through FFFFFH(16bytes) these areas are used for interrupt and system reset processing 8086 and 8088 application systems should not use these areas for any other system purposes
  - in modern linux it start with start_kernel() https://elixir.bootlin.com/linux/v4.14.320/source/init/main.c#L512






























### Tools
- ptrace
 

#### Some source and book
- The Art of Linux Kernel  
- Computer Architecture  
- Understanding The Linux
- Assembly Language Step by Step
- Operating Systems Internals and Design Principles
- MINIX3
- uefi.org/uefi
- BIOS Boot Specification Version 1.01
- github.com/rhboot/grub2
- [unix source code](http://v6.cuzuco.com/v6.pdf)
- [linux,unix, bsd tour](https://www.tamacom.com/tour/kernel/unix/)
- https://github.com/rhboot/grub2/blob/fedora-39/grub-core/boot/i386/pc/boot.S
- https://0xax.gitbooks.io/linux-insides/content/
- https://www.kernel.org/doc/Documentation/x86/boot.txt
- https://www.linuxfromscratch.org/
- https://0pointer.de/blog/projects/systemd.html
- https://lwn.net/Articles/250967/
- https://linux-mm.org/LinuxMM
- https://kernelnewbies.org/KernelProjects
- https://www.intel.com/content/dam/www/public/us/en/documents/manuals/64-ia-32-architectures-software-developer-vol-1-manual.pdf
- https://www.intel.com/content/dam/www/public/us/en/documents/manuals/64-ia-32-architectures-software-developer-system-programming-manual-325384.pdf
- https://yasm.tortall.net/
- https://www.bottomupcs.com/
- really helpful one, https://github.com/ianw/bottomupcs/tree/master
- C Programming Languages
    - http://infolab.stanford.edu/~ullman/focs.html
    - https://www.cs.rit.edu/~ats/books/ooc.pdf
    - https://www.cs.rit.edu/~ats/books/
