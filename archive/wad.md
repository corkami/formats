Doom's "Where's All the Data"


# Doc

[wadread.c](https://github.com/id-Software/DOOM/blob/master/sndserv/wadread.c#L57)


# Format


## Structure

A header at offset 0, points to a list of lump directories, which points to lumps (file data).

```
Header -> filelumps*
```	

All numbers are 4 bytes, little endian, signed (limited to 2^31 - 1).


## Header

*wadinfo_t*:
- 00+4 *identification*:  `.I .W .A .D` (internal) or `.P .W .A .D` (patch)
- 04+4 *numlumps*: number of lumps
- 08+4 *infotableofs*: offset of the directories
- 0C


## Directory

*filelump_t*:
- 00+4 *filepos*: pointer to file data
- 04+4 *size*: size of file data
- 08+8 *name*: 0-padded, alphanum, uppercase, 8 byte long
- 10
