- http://www.libtiff.org/ - `tiffdump`
- https://www.adobe.io/open/standards/TIFF.html
  - TIFF6.pdf Specifications for TIFF...
  - TIFFPM6.pdf TIFF technical notes.
  - TIFFphotoshop.pdf Description of the compression schemes provided by the Adobe Photoshop® “Advanced TIFF” options dialog.


# Structure

Image File Header, at offset `0`
```
 0     2     4          8
Si Si Nu Nu Of Of Of Of
```
- 00+2: Signature `MM` or `II` to define big or little endianness.
- 02+2: Number 0x42 with the right endianness
- 04+4: Offset to the next Image File Directory.

followed by image data


Image File Directory
```
Nu Nu (DirectoryEntries*) Of Of Of Of
```
- 00+2: number of Directory Entries
- 02+12*x: Directory Entries
- ??+4: Offset to next IFD


Directory Entries
```
 0     2     4  5  6     8           C
Ta Ta Ty Ty Co Co Co Co VO VO VO VO
```
- 00+2: Tag
- 02+2: Type 
- 04+4: Count
- 08+4: Value/Offset (`value` if `type*count` fits in 4 bytes, else `offset`)
