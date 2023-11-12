 ```bash
 ./a.out &
 ps  
#  get  pid : xxx
  pmap 80842 > pmap.log
  kill 80842
  
#   this file store the map
  /proc/80842/maps

#!   or use gdb make the program trap into stop status and find the pid of that program.
 ```


 diff of  a running linux-user-program-address-space and a executable a.out file:

  The memory layout of a process includes **not only the code and data from the binary file**, but also any shared libraries the process is using, the process’s stack, and any memory the process has dynamically allocated. 


  a.out parse by objdump get: computation(logic) and data 

 Text segment: This is where the actual code of the program resides.  
Data segment: This is for global and static variables initialized by the programmer.  
BSS (Block Started by Symbol)segment: This holds uninitialized global and static variables.  
Heap: This is for dynamic memory allocation during the process runtime.  
Stack: This is used for local variables and for maintaining the function call-return structure.  

bss: . It’s a term that originated from an IBM assembler program, where it was used to reserve space for variables1. In the context of C programming and many other languages, the BSS segment is a portion of an object file or executable that contains statically allocated variables that are declared but have not been assigned a value yet1.


# Load the a.out into memory and run :
the running program address-space become: 

The kernel code segment (__KERNEL_CS)   
The kernel data segment (__KERNEL_DS)  
  
and the a.out code ,data segment .

code include : text seg,stack(include part of current point of code and data )  
data include : data seg , heap , 

# modify a running process address space 
ref: https://jyywiki.cn/OS/2023/build/lect17.ipynb.html
```c
// 映射
void *mmap(void *addr, size_t length, int prot, int flags,
           int fd, off_t offset);
int munmap(void *addr, size_t length);

// 修改映射权限
int mprotect(void *addr, size_t length, int prot);
```




