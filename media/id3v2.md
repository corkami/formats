
ID3 v2.3.0

Doc: https://id3.org/id3v2.3.0

Dissector: ffprobe -show_frames

Structure: `Header ExtendedHeader? Frames+`


Header (at offset 0):

```
 0        3  4  5  6           A
.I .D .3 03 00 Fl Si Si Si Si
```

- 00+4 ID3 identifier
- 03+2 Version (always `03 00` for this ID3)
- 05+1 Flags abc00000
  - a:7 unsynchronisation
  - b:6 extended header
  - c:5 experimental
- 06+4 Size (7-bits)  0xxxxxxx

Extended header:
```
 0           4     6           A
Si Si Si Si Fl Fl Pa Pa Pa Pa
```

- 00+4 Extended header Size
- 04+2 Extended Flags x0000000 00000000
  - x:1 CRC present
- 06+4 Size of padding

Frame:
```
 0           4           8     A
Id Id Id Id Si Si Si Si Fl Fl Da*
```

- 00+4 Identifier
- 04+4 Size
- 08+2 Flags abc00000 ijk00000
 - a Tag Alter preservation
 - b File Alter preservation
 - c Read Only

 - i Compression
 - j Encryption
 - k Grouping identity
- 0A:? Data (layer 3 frames)


The ID of all frames of text begin with T except `TXXX`

Text is a sequence of `EE <text>`:
EE is encoding: `00` for ISO-8859-1, `01` for Unicode.
