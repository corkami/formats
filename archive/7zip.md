7z

Software = `7-zip`
Format = `7z`

- https://www.7-zip.org/sdk.html
- https://py7zr.readthedocs.io/en/stable/archive_format.html
- 7zFormat.txt

Variable length integers

Structure: SignatureHeader PacketStreams* 

Signature Header:
- Signature `.7 .z bc af 27 1c`
- Major Version, BYTE, '0x00'
- Minor Version, BYTE, '0x04'
- Start Header CRC, UINT32
- Next Header Offset, NUMBER (Absolute - 32)
- Next Header Size, NUMBER
- Next Header CRC, UINT32
