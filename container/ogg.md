Ogg Container (transport bitstream)


# Ogg

Formats: Vorbis, Opus, Ogg Flac, Theora, Dirac

https://en.wikipedia.org/wiki/Ogg_page
https://xiph.org/vorbis/doc/framing.html

Tool: oggz-dump


# Structure

File: `page*`

Ogg page:
```
00          04 05 06                      0E   
MM MM MM MM VV TT GP GP GP GP GP GP GP GP BN BN
      12          16          1A 1B
BN BN PN PN PN PN CS CS CS CS CO ST
```

- 00+4 Magic `OggS`
- 04+1 Version `00`
- 05+1 Type (1=continuation, 2=first, 4=last)
- 06+8 Granule position
- 0E+4 Bitstream Serial Number
- 12+4 Page Sequence Number
- 16+4 CRC Checksum (direct, init and xor=0, poly=`0x04c11db7`) - it's required by VLC, not MPV
- 1A+1 Segments count
- 1B   Segment table

Segment table: `LL*` (8b length of each segment)