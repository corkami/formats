A simple binary serialisation format

# Resource Interchange File Format

https://en.wikipedia.org/wiki/Resource_Interchange_File_Format

Exists in Big Endian, RIFX

Formats:
- WAV (Waveform Audio format)
- AVI (Audio Video Interleave)
- ANI (Windows/Cursor animation)
- CDR (Corel Draw), WebP (images)
- BuNDle
- SfBk (SoundFont Banks)
- RDIB (Device Independant Bitmap)
- RMI (Riff Midi)
- RMMP
- PAL (palette)
- DLS
- XMA
- CdIx (LLVM symbols)



## Structure

File structure (at offset zero):

```
00          04          08          0C
.R .I .F ?? SS SS SS SS TT TT TT TT C?
```

- 00+4 Signature: RIFF (little endian) or RIFX (big endian)
- 04+4 File Size - 8
- 08+4 File Type (WAVE, AVI\x20, ...)
- 0C: sequences of chunks


ChunkL
```
00          04          08
II II II II LL LL LL LL D? P?
```
- 00+4 ID
- 04+4 Length (of file en)
- 08+? Data
- ??+? Padding (word alignment)


`LIST` is a special chunk ID containing no data per se but sub-chunks,
which actually follows the same structure as the RIFF file
(so it can be said to be another special chunk, used only for the overall file)

```
00          04          08          0C
.L .I .S .T LL LL LL LL TT TT TT TT C?
```
 
`JUNK` is an official chunk name.

RIFF files can be compound which implies at topmost level
- a `CTOC` chunk (Compound File Table of Contents) <- to be updated?
- a `CGRP` chunk (Compound File Element Group)


## Wave

WAV uses PCM by default, but many other [codecs](https://tools.ietf.org/html/rfc2361) including MP3

http://www-mmsp.ece.mcgill.ca/Documents/AudioFormats/WAVE/WAVE.html
http://www-mmsp.ece.mcgill.ca/Documents/AudioFormats/WAVE/Docs/riffmci.pdf
