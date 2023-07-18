## understanding linux 0.11 internal


### Booting 
- everything is start from 0xFFFF0 => boots/bootsect.s  
    - it start with assembly/hardware language not c language cause ram and cpu even didn't start.  
    - As a general rule, the Linux kernel is installed in RAM starting from the physical address 0x00100000  
    - what it means? One way to implement NOT is to use XOR with one operand being all ones (FFFF FFFF FFFF FFFFhex).  
    - Page frame 0 is used by BIOS to store the system hardware configuration
detected during the Power-On Self-Test (POST); the BIOS of many laptops,
moreover, writes data on this page frame even after the system is initialized.  
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


- in modern linux it start with start_kernel() https://elixir.bootlin.com/linux/v4.14.320/source/init/main.c#L512










#### Source Book
- The Art of Linux Kernel  
- Computer Architecture  
- Understanding The Linux
- MINIX3
