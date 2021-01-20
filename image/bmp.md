Extensions: BMP, RLE, LGO

# File header

```
 0     2           6  7  8          12
Ma Ma Fs Fs Fs Fs Hx Hy Of Of Of Of 
```

- 00+2: Magic
  - `BM`: Bitmap
  - `BA`: Bitmap Array
  - `CI`: Color Icon
  - `CP`: Color Pointer
  - `IC`: Icon
  - `PT`: Pointer
- 02+4: :File size - not necessarily correct nor validated
- 06+1: Hotspot X - ignored for BMP
- 07+1: Hotspot Y - ignored for BMP
- 08+4: Offset to data =BOF
- 12: Bitmap header


# Bitmap header

```
 0           4     6     8    10    12
Si Si Si Si Wi Wi He He Np Np Bp Bp|
```

- 00+4: Header size - also distinguishes versions
  -  12: OS/2 1.x - Core
  -  40: Windows 3.x - Info
  -  52: Photoshop - Info v2
  -  56: Photoshop w/ transparency - Info v3
  -  64: OS/2 2.x
  - 108: Windows 95/NT4 - v4
  - 124: Windows 98/2000 - v5
  - 128: Windows NT/2000
- 04+2: Width
- 06+2: Height
- 08+2: NumPlanes
- 10+2: BitsPerPixel =BPP
- 12+4: Bitmap compression scheme
- 16+4: Size of bitmap data in bytes
- 20+4: X resolution
- 24+4: Y resolution
- 28+4: Number of color table indices used
- 32+4: Number of important color indices
- 36+2: Type of units used to measure resolution
- 38+2: Pad structure to 4-byte boundary
- 40+2: Recording algorithm
- 42+2: Halftoning algorithm used
- 44+4: Reserved for halftoning algorithm use
- 48+4: Reserved for halftoning algorithm use
- 52+4: Color model used in bitmap
- 56+4: Reserved for application use
- 60
