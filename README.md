# Operating System 
# Assignment # 01
- Name : Muhammad Subhan Khurshid
- RollNo : 21k-3096
## Adding a Hello World System Call
## Preparations

#### 1. Update Your System:
By adding the following commands update/upgrade your system first.
- sudo apt-get update
- sudo apt-get upgrade

#### 2. Download Packages To Compile The Kernel:
- sudo apt install build-essential libncurses-dev libssl-dev libelf-dev bison flex-y
And we need and extra package which dwarves We will install it by typing sudo apt install dwarves (Compiltion occurs when we dont have this package).

#### 3. Download The Kernel:
Download the kernel from kernel.org.
wget -P ~/ https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.8.1.tar.xz

<img width="552" alt="Picture1" src="https://user-images.githubusercontent.com/105592966/221379072-7d5b9df2-14f9-4dea-9aa0-1c8dfb841de7.png">

#### 4. Extract The Kernel:
tar -xvf ~/linux-5.8.1.tar.xz -C ~/

<img width="554" alt="Picture2" src="https://user-images.githubusercontent.com/105592966/221379090-661d3da0-b7e2-430d-ae62-88df1732aeb3.png">


## Creation

#### 1. Change Your Working Directory:
cd ~/linux-5.8.1/

##### 2. Make a Folder For Your System Call:
mkdir HelloWorld

#### 3. Create a C File For Your System Call:
nano HelloWorld/HelloWorld.c

- Write the following code in it:

#include<linus/syscall.h> 
SyscallDefine0(HelloWorld) {
printk("Hello world.\n");
return 0;
}

##### Code Explanation:
- We used #include <linux/kernel> because we are building a system call for our linux 
kernel.
- Amslinkage simply means that the arguments for this function will be on the stack 
instead of the CPU registers.
- Printk is used instead of printf because we are going to print in the kernel’s log file.
- If the code is run and it returns 0, then it will mean that our program ran successfully 
and Hello world is written to out kernel’s log file.

#### 4. Create a File For Your System Call;
nano HelloWorld/Makefile
Paste this in makefile
obj-y := HelloWorld.o

<img width="421" alt="Picture4" src="https://user-images.githubusercontent.com/105592966/221379378-2a00b86d-8d00-4517-bd9f-ca5ceb229233.png">



#### 5. Edit The MakeFile:
Change the version to your roll number
SEARCH core-y
Replace pervious with this
kernel/ certs/ mm/ fs/ ipc/ security/ crypto/ block/ HelloWorld/

#### 6. Open Header File and add asmlinkage :
At the bottom of asmlimkage file before endif
asmlinkage long sys_HelloWorld(void)

<img width="413" alt="Picture5" src="https://user-images.githubusercontent.com/105592966/221379414-b6079ac9-ccee-4a89-b742-f3000cc6d9e5.png">

#### 7. Adding the prototype of the new system call into the system calls header file:
Now we have to add the prototype of our system call in the system’s header file which is 
located in the kernel folder then “/include/linux/syscalls.h”. We have to add the prototype 
of our system call function in this file.

<img width="416" alt="Picture6" src="https://user-images.githubusercontent.com/105592966/221379464-869c4ca2-69a0-402c-9179-8a8ccaf45cc1.png">

## Installation:
Run the following commands for the installation
- Sudo make menuconfig
- scripts/config --disable SYSTEM_REVOCATION_KEYS
- scripts/config --disable SYSTEM_TRUSTED_KEYS
- Sudo make
- sudo make modules
- sudo make modules_install
- sudo make install
Then if an error occurs which says make bzImage
- sudo make bzImage
- Then sudo install
- sudo update-grub
- Restart

## Results:

- nano report.c
- Paste the code
#include <linux/kernel.h>
#include <sys/syscall.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>
#define __NR_HelloWorld 440
long HelloWorld_syscall(void)
{
return syscall(__NR_HelloWorld);
}
int main(int argc, char *argv[])
{
long activity;
activity = HelloWorld_syscall();
if(activity < 0)
{
perror("system call failed.");
}
else
{
printf("System call worked \n");
}
return 0;
}
Compile and run the program
gcc -o report report.c
./report
Dmesg


