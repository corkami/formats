Flac (native - exists also in Ogg container)

Free Lossless Audio Codec

https://xiph.org/flac/documentation_format_overview.html

# Structure

File: `Magic StreamInfoBlock Blocks* AudioFrames+`
``` 
00          04
MM MM MM MM 
```
- 00+4 Magic `fLaC`
- 04   StreamInfo block

Block: `Header then data`
```
00 01       04
LT LL LL LL D?
```
- 00+1 Last block / block type  bitmask
  - 1 last block
  - 7 type: 0=streaminginfo, 1=padding, 2=application, 3=seektable, 4=comment
- 01+3 block data length
- 04+? block data

Application:
- 00+4 Registered ID
- 04+? data
