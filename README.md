# NuOsTheorySpring23

## Adding a Hello World System Call To Your Kernel
## OPERATING SYSTEM
## Assignment - 01

- Name : Muhammad Subhan Khurshid
- RollNo : 21k-3096

## Prerequisites:
- sudo apt-get install gcc
- sudo apt-get install libncurses5-dev
- sudo apt-get install bison 
- sudo apt-get install flex
- sudo apt install make
- sudo apt-install libssl-dev
- sudo apt-get install libelf-dev 
- sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main 
  universe"
- sudo apt-get update
- sudo apt-get upgrade 


# STEPS:
## 1. Downloading Kernel:
First of all, we have to download a kernel from kernel.org. We can either do this by using the 
“wget” command or download it manually by clicking the “tarball” option.


<img width="552" alt="Picture1" src="https://user-images.githubusercontent.com/105592966/221367204-a4a5d576-016e-4044-a171-3d9d32da4fec.png">

## 2. Extracting The Kernel :
Now, go to the folder where the kernel is downloaded and extract it by typing “tar -xvf 
*filename*” or simply by right clicking it and selecting the “extract to” option

<img width="554" alt="Picture2" src="https://user-images.githubusercontent.com/105592966/221367275-19bfe0f8-bba7-440b-91eb-bdd87fc73b77.png">


## 3. Making a New Folder called Hello :
Go into the folder where you extracted the kernel and go inside the kernel’s folder and 
create a new directory by either opening the terminal there and typing “mkdir *folder 
name*” or simply by right clicking there and clicking on new folder

<img width="554" alt="Picture3" src="https://user-images.githubusercontent.com/105592966/221367340-7d334ae6-2ad4-4ab4-b1f2-78cc0faea2b6.png">


## 4. Adding a C code for the system call :
Now, go to the folder which we created just now and open the terminal there and create a 
new C code file by typing “gedit hello.c” and paste the following code there:

#include < inux/kernel.h >
AsmLinkage long sys_hello(void) 
{
    printf("Hello World/n");
    return 0;
}

## Code Explaination:
- We used #include <linux/kernel> because we are building a system call for our linux 
kernel.
- Amslinkage simply means that the arguments for this function will be on the stack 
instead of the CPU registers.
- Printk is used instead of printf because we are going to print in the kernel’s log file.
- If the code is run and it returns 0, then it will mean that our program ran successfully 
and Hello world is written to out kernel’s log file

## 5. Creating a MakeFile for the C Code:
ow, we have to create a Makefile for our new folder to ensure that the code in the folder is 
always compiled whenever the kernel is compiled. In order to do this, we type in our 
terminal “gedit Makefile” and put “obj-y := hello.o”

<img width="421" alt="Picture4" src="https://user-images.githubusercontent.com/105592966/221369096-1269d95e-e04c-48be-9308-e8efcebc0ce8.png">


## 6. Adding The NewCode into the System Table File:
Since we are creating a 64-bit system call according to our system we have to add the 
system call entry into the syscall_64.tbl file which keeps the name of all the system calls in 
our system. If our system was a 32-bit system, we would have to add our system call into 
syscall_32.tbl (We can check the type of our system by typing “uname -m” in a terminal). 
This tbl file is located inside the kernel folder in /arch/x86/entry/syscalls/syscall_64.tbl. We 
can go into this directory by using cd and then edit the file by typing “gedit syscall_64.tbl”




<img width="413" alt="Picture5" src="https://user-images.githubusercontent.com/105592966/221369168-8f6230e3-fa49-451e-a6d4-6ff285569447.png">
