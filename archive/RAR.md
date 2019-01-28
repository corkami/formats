# Roshal Archive

- [Rar 1.34b](https://www.virustotal.com/#/file/6e09a221115efd7f2a9a468fb41f1f014b08472ca854ef615f838b84d8eefec5) (from [old-dos.ru](http://old-dos.ru/files/file_696.html))
- UnRAR: archive.cpp [RARFORMAT Archive::IsSignature](https://github.com/adamhathcock/sharpcompress/blob/master/reference/unrar/archive.cpp#L97)
- [Specifications](https://www.rarlab.com/technote.htm)
- [Know your archive: ​Rosha ARchive (​RAR)](http://jasonblanks.com/wp-includes/images/papers/KnowyourarchiveRAR.pdf)
- libmagic: [`RE\x7e\x5e`: RAR archive data (<v1.5)](https://github.com/file/file/blob/master/magic/Magdir/archive#L1001)
- [Python module for RAR archive reading](https://github.com/markokr/rarfile)

# PoCs

smallest

v1.4:
```
00: .R .E .~ .^ 07 00 C0 00 00 00 00 00 00 00 00 00
10: 00 16 00 A0 A9 84 4D 20 00 02 01 05 .N
```

v4:
```
00: .R .a .r .! 1A 07 00 CF 90 73 00 00 0D 00 00 00
10: 00 00 00 00 3F 1E 74 00 80 21 00 00 00 00 00 00
20: 00 00 00 00 00 00 00 00 07 63 66 4D 0F 33 01 00
30: 20 00 00 00 .n
```

## v1.4
```
HEAD_ID:4c;
  HEAD_LEN:<2; HEAD_FLAGS;1;
  COMM_LEN[bVolume]:1; MAIN_COMMENT:[COMM_LEN];
```

HEAD_ID: `52 45 7e 5e`

HEAD_FLAGS:
1. `1` bVolume
1. `2` bComment
1. `4` bProtected
1. `8` bSolid

## File
```
PACK_LEN:<4; UNP_LEN:<4; CHECKSUM:<2;
  HEAD_LEN:<2; FTIME:4; ATTR:1; VER:1; NAME_LEN:1; METHOD:1;
  FILE_COMM_LEN[bComment];1; FILE_COMMENT;[FILE_COMM_LEN]; FILENAME;[NAME_LEN]c;
```

VER:
1. `0` Rar 0.99
2. `1` Rar 1.00
3. `2` Rar 1.30


FLAGS:
1. `1` bPrevious
2. `2` bNext
3. `4` bPassword
4. `8` bComment
