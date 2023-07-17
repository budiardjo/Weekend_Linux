## understanding linux 0.11 internal

- everything is start from 0xFFFF0 => boots/bootsect.s  
- what it means? One way to implement NOT is to use XOR with one operand being all ones (FFFF FFFF FFFF FFFFhex).  

- it start with assembly/hardware language not c language cause ram and cpu even didn't start  
