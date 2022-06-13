Unix `archiver` ar

https://en.wikipedia.org/wiki/Ar_(Unix)

```
FileName/       TimeStamp   Owner Group Perms   FileSize  60\n
hello.txt/      0           0     0     644     13        `
0+16            16+12       28+6  34+6  40+8    48+10     58+2
```

All fields with right padding with space.

Long filename variant:
 file name is stored after the data, and
 file name length is stored after the forward slash in the filename
  so `#1/0` is a null filename


EBNF [grammar](https://www.bottlecaps.de/rr/ui):
```
ARchive  ::= 'Signature:8' (('Identifier:16' 'mTime:12' 'OID:6' 'GID:6' 'Mod:8' 'Size:10' 'Trailer:2') FileData)+
```
