Windows Icons .ICO, .CUR cursors

Structure:
Header then image directories

ICONDIR
```
00    02    04    06
Re Re TT TT CC CC
```
- 00+2 Reserved (must be 0)
- 02+2 Type (icon = 1, cursor = 2)
- 04+2 Image count
Size:06

ICONDIRENTRY:
```
00 01 02 03 04    06    08          0C          10
Wi He PC Re Pl Pl Bp Bp Si Si Si Si Of Of Of Of
```
- 00+1 Width
- 01+1 Height
- 02+1 Palette Colors (0 if no palette is used)
- 03+1 Reserved (0)
- 04+2 Planes
- 06+2 Bits per pixel
- 08+4 Size
- 0C+4 offset

size: 10
