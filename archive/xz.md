[Specs](https://tukaani.org/xz/xz-file-format-1.0.4.txt)


```
XZ ::= (Stream Padding)+

Stream ::= StreamHeader Block+ Index StreamFooter

StreamHeader ::= Magic6 'Flags:2' 'CRC32:4'

Magic6 ::= '"0xFD 7zXZ 0x00"'

StreamFooter ::= 'CRC32:4' 'BackwardSize:4' 'Flags:2' Magic2

Magic2 ::= '"YZ"'

Block ::= BlockHeader Data Padding Check

BlockHeader ::= BlockHeaderSize Flags CompressedSize UncompressedSize FilterFlags Padding 'CRC32:4'

FilterFlags ::= FilterFlag*

FilterFlag ::= ID PropertiesSize Properties

Index ::= Indicator NumberOfRecords Records* Padding 'CRC32:4'

Record ::= UnpaddedSize UncompressedSize
```
