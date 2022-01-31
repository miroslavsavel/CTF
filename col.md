https://bk1603.github.io/posts/writeups/fd/

scp -r -P2222 fd@pwnable.kr:~/ ./
ssh ukoncim prikazom
$exit


Daddy told me about cool MD5 hash collision today.
I wanna do something like that too!
>> kali linux /CTF/Col/col

hexa vystup printf
https://stackoverflow.com/questions/14733761/printf-formatting-for-hexadecimal
	printf("dec check_password : %d \n", check_password( p));
	printf("hex check_password : %#010x \n", check_password( p));

aaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaab
baaaaaaaaaaaaaaaaaaa
AAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAB
00000000000000000000
llllllllllllllllllll
abababababababababab
lzmllzmllzmllzmllzml
ääääääääääääääääääää

gcc -g test.c
./a.out aaaaaaaaaaaaaaaaaaaa


po vypocte
21DD09EC ÷ 5 = 6C5CEC8 Remainder : 4
tzäztzäztzäztzäztzäz

skusim to opacne zapisat little endian
zäztzäztzäztzäztzäzt


https://jaimelightfoot.com/blog/pwnables-kr-collision-walkthrough/

0x21DD09EC - 0x06C5CEC8 * 4 = our leftovers
0x21DD09EC - 0x1B173B20 = our leftovers = 0x06C5CECC

Double-checking:

0x06C5CEC8 * 4 + 0x06C5CECC = 0x21DD09EC

cize v endiane budu tieto znaky naopak
0x06C5CEC8 => 0xC8 0xCE 0xC5 0x06
0x06C5CECC => 0xCC 0xCE 0xC5 0x06


prislusne hodnoty ASCI znakov si vyrobim pomocou python skriptu
https://askubuntu.com/questions/1195561/what-does-c-or-m-mean-in-the-command-line

python -c 'print("AHOJ")'  


./col "`python -c "print '\xc8\xce\xc5\x06'*4+'\xcc\xce\xc5\x06'"`"
