# Zlib

ZLIB encapsulate Deflate blocks.


# Deflate

Deflate is PKZip's algorithm, by Phil Katz.


## CRC

Deflate's CRC32 is:
 - polynomial: `x^32 + x^26 + x^23 + x^22 + x^16 + x^12 + x^11 + x^10 + x^8 + x^7 + x^5 + x^4 + x^2 + x + 1`
 - parameters:
   - Input & result reflected
   - polynomial: `0x04C11DB7`
   - initial value and final xor: `FFFFFFFF`


# links

Implementations:
- [zlib](https://zlib.net/)
- [7zip](https://www.7-zip.org/7z.html)
- [Zopfli](https://github.com/google/zopfli)

Other:
- Gabor Molnar's [ascii-zip](https://github.com/molnarg/ascii-zip)
