gzip

https://tools.ietf.org/html/rfc1952

```
00    02 03 04          08 09 10
MM MM CC FF TT TT TT TT XX OO [LL LL DD?] [NN 00] [cc 00] [RR RR]
```

- 00 MM:2 Magic `1F 8b`
- 02 CM:1 Compression method 8:deflate
- 03 FF:1 Flags FTEXT:1 FHCRC:1 FEXTRA:1 FNAME:1 FCOMMENT:4 reserved:3
- 04 TT:4 Modification time
- 08 XX:1 Extra flags
- 09 OS:1

if FEXTRA
- LL:2 Extra length
- DD:? Extra field

if FNAME
- NN:? Name (0-terminated)

if FCOMMENT
- cc:? Commment (0-terminated)

if FCRC
- RR:2 CRC16
