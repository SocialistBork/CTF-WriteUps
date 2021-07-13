# PicoCTF 2021
Ctf At: https://ctf.redpwn.net/

## wstrings
### Challenge Description
Category: Reverse Engineering

Description: Some strings are wider than normal...

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
