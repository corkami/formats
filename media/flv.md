Flash Video
https://www.adobe.com/content/dam/acom/en/devnet/flv/video_file_format_spec_v10.pdf

FLV Header
```
00       03 04 05          09
Ma Ma Ma Ve Fl Da Da Da Da
```
- 00+3 Magic `FLV`
- 03+1 Version `01`
- 04+1 Reserved:5 Audio:1 Reserved:1 Video:1
- 05+4 Data offset
