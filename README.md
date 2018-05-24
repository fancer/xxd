# xxd
This is well known hex-dump-type utility distributed as a part of vim-project. The program manual states: make a hexdump or do the reverse, which is the main features of the utility. It can do nearly everything hexdump can and moreover perform the reversal translation of hex-like text back to binary representation. Like  uuencode and uudecode it allows the transmission of binary data in a `mail-safe' ASCII representation, but has the advantage of decoding to  standard output.  Moreover, it can be used to perform binary file patching.

## Usage
Print everything but the first three lines (hex 0x30 bytes) of file.
```
% xxd -s 0x30 file
```

Print 3 lines (hex 0x30 bytes) from the end of file.
```
% xxd -s -0x30 file
```

Print 120 bytes as continuous hexdump with 20 octets per line.
```
% xxd -l 120 -ps -c 20 xxd.1
2e54482058584420312022417567757374203139
39362220224d616e75616c207061676520666f72
20787864220a2e5c220a2e5c222032317374204d
617920313939360a2e5c22204d616e2070616765
20617574686f723a0a2e5c2220202020546f6e79
204e7567656e74203c746f6e79407363746e7567
```

Hexdump the first 120 bytes of this man page with 12 octets per line.
```
% xxd -l 120 -c 12 xxd.1
0000000: 2e54 4820 5858 4420 3120 2241  .TH XXD 1 "A
000000c: 7567 7573 7420 3139 3936 2220  ugust 1996"
0000018: 224d 616e 7561 6c20 7061 6765  "Manual page
0000024: 2066 6f72 2078 7864 220a 2e5c   for xxd"..\
0000030: 220a 2e5c 2220 3231 7374 204d  "..\" 21st M
000003c: 6179 2031 3939 360a 2e5c 2220  ay 1996..\"
0000048: 4d61 6e20 7061 6765 2061 7574  Man page aut
0000054: 686f 723a 0a2e 5c22 2020 2020  hor:..\"
0000060: 546f 6e79 204e 7567 656e 7420  Tony Nugent
000006c: 3c74 6f6e 7940 7363 746e 7567  <tony@sctnug
```

Display just the date from the file xxd.1
```
% xxd -s 0x36 -l 13 -c 13 xxd.1
0000036: 3231 7374 204d 6179 2031 3939 36  21st May 1996
```

Copy input_file to output_file and prepend 100 bytes of value 0x00.
```
% xxd input_file | xxd -r -s 100 > output_file
```

Patch the date in the file xxd.1
```
% echo "0000037: 3574 68" | xxd -r - xxd.1
% xxd -s 0x36 -l 13 -c 13 xxd.1
0000036: 3235 7468 204d 6179 2031 3939 36  25th May 1996
```

Create a 65537 byte file with all bytes 0x00, except for the  last  one which is 'A' (hex 0x41).
```
% echo "010000: 41" | xxd -r > file
```

Hexdump this file with autoskip.
```
% xxd -a -c 12 file
0000000: 0000 0000 0000 0000 0000 0000  ............
*
000fffc: 0000 0000 40                   ....A
```

Create  a  1  byte  file containing a single 'A' character.  The number
after '-r -s' adds to the linenumbers found in the file; in effect, the
leading bytes are suppressed.
```
% echo "010000: 41" | xxd -r -s -0x10000 > file
```

Read single characters from a serial line
```
% xxd -c1 < /dev/term/b &
% stty < /dev/term/b -echo -opost -isig -icanon min 1
% echo -n foo > /dev/term/b
```

## Features

There is a whole set of features that make xxd more useful than traditional hexdump in some cases:
  * Reverse translation (ASCII-binary-ASCII)
  * Continuous (plain) hexdump
  * Seeking input/output file
  * Less xxd binary size than hexdump one
  * Endian conversion
  * ...

## Motivation

It was surpizing for me, that the xxd utility was distributed as a part of vim-project and its packages. What if I didn't need the whole vim editor, but just xxd functionality? This was my case, when I needed the reverse translation feature, but didn't want the editor being built/installed on my system due to a memory limitation. In addition, if hexdump is better for various representations of output data, I find xxd feature reacher. The fact, that xxd prodice smaller execution binary, makes it to be the best candidate for embedded systems. So I decided to create a seperate configuration/installation package for xxd only.

Original utility code was taken from: [vim github repo](https://github.com/vim/vim) at the state of tag v8.1.0000

(xxd code copyrights are left untouched as well as the license declaration. This package is licensed by GPL-2.0 so to make it compatible with original utility)
