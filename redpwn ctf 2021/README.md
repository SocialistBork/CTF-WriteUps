# PicoCTF 2021
Ctf At: https://ctf.redpwn.net/

## wstrings
### Challenge Details
**Category:** Reverse Engineering

**Description:** Some strings are wider than normal...

### Solution
A simple hexdump will reveal that the flag is inbedded in the file's code. You can use the hexedit command on Linux. 
Alternatively, you can use "Open with Notepad" on Windows.

```
00000930  01 00 02 00 00 00 00 00 66 00 00 00 6c 00 00 00  |........f...l...|
00000940  61 00 00 00 67 00 00 00 7b 00 00 00 6e 00 00 00  |a...g...{...n...|
00000950  30 00 00 00 74 00 00 00 5f 00 00 00 61 00 00 00  |0...t..._...a...|
00000960  6c 00 00 00 31 00 00 00 5f 00 00 00 73 00 00 00  |l...1..._...s...|
00000970  74 00 00 00 72 00 00 00 31 00 00 00 6e 00 00 00  |t...r...1...n...|
00000980  67 00 00 00 73 00 00 00 5f 00 00 00 61 00 00 00  |g...s..._...a...|
00000990  72 00 00 00 33 00 00 00 5f 00 00 00 73 00 00 00  |r...3..._...s...|
000009a0  6b 00 00 00 31 00 00 00 6e 00 00 00 6e 00 00 00  |k...1...n...n...|
000009b0  79 00 00 00 7d 00 00 00 00 00 00 00 00 00 00 00  |y...}...........|
```
The letters of the actual flag are seperated with 3 characters, so filter out the other characters to get the flag.
```
flag{n0t_al1_str1ngs_ar3_sk1nny}
```

## baby
### Challenge Details
**Category:** Crypto

**Description:** I want to do an RSA!

### Solution
The file provided has this information: 
```
n: 228430203128652625114739053365339856393
e: 65537
c: 126721104148692049427127809839057445790
```
If it isn't apparent already, this problems is about RSA. If you do not know what RSA is, refer to this: https://www.educative.io/edpresso/what-is-the-rsa-algorithm.
First, factor out N, which is the product of the primes p and q. You can use http://factordb.com/ to find them.

You can use a script to solve this problem.
```
from Crypto.Util.number import long_to_bytes
import libnum
import sys

p=18207136478875858439
q=12546190522253739887
c=126721104148692049427127809839057445790
#N=228430203128652625114739053365339856393

if (len(sys.argv)>1):
        c=int(sys.argv[1])
if (len(sys.argv)>2):
        p=int(sys.argv[2])
if (len(sys.argv)>3):
        q=int(sys.argv[3])

n = p*q
PHI=(p-1)*(q-1)

e=65537
d=(libnum.invmod(e, PHI))


res=pow(c,d, n)

print ("Cipher: ",c)
print ("p: ",p)
print ("q: ",q)

print ("\n=== Calc ===")
print ("d=",d)
print ("n=",n)
print ("Decrypt: %s" % ((long_to_bytes(res))))
```
Altenatively, you can use https://www.dcode.fr/rsa-cipher to decode the cipher text. Both results will give you the flag.

```
flag{68ab82df34}
```
