
The official [specifications](APPNOTE.md) don't provide any official (short and usable) name.

A ZIP without any file is offically valid and empty.

Ex, line 603:
```text
   4.3.16  End of central directory record:

      end of central dir signature    4 bytes  (0x06054b50)
      number of this disk             2 bytes
      number of the disk with the
      start of the central directory  2 bytes
      total number of entries in the
      central directory on this disk  2 bytes
      total number of entries in
      the central directory           2 bytes
      size of the central directory   4 bytes
      offset of start of central
      directory with respect to
      the starting disk number        4 bytes
      .ZIP file comment length        2 bytes
      .ZIP file comment       (variable size)
```

The 7th member of the structure called *End of central director record*
is only described as *offset of start of central directory with respect to the starting disk number*.
It has no other name whatsoever.

Of course, in practice, there is a need for a shorter structure name:
- in [7Zip](https://github.com/kornelski/7z/blob/master/CPP/7zip/Archive/Zip/ZipIn.h#L125) this is the `Offset` member of the `CCdInfo` structure.
- in [zlib](https://github.com/madler/zlib/blob/master/contrib/minizip/zip.c#L646), this is called `offset_central_dir`;

other sources:
- [ZipStream](https://github.com/SpiderOak/ZipStream)
- Java [ZipFile](http://developer.classpath.org/doc/java/util/zip/ZipFile-source.html)

# structure layout

- spanning archive sig      `PK\x07\x08`
- temporary spanning sig    `PK\x03\x03`
- **local file header**     `PK\x03\x04`
 - file name
 - extra field
 - encryption header
 - file data
 - data descriptor          `PK\x07\x08` (optional!)
- archive decryption header
- archive extra data record `PK\x06\x08`
- **central directory**     `PK\x01\x02`
 - file name
 - extra field
 - file comment
- zip64 EoCD                `PK\x06\x06`
- zip64 EoCD locator        `PK\x06\x07`
- **EoCD**                  `PK\x05\x06`
 - archive comment
- digital signature         `PK\x05\x05`


from the doc:

Local File Headers (1 per file) *sequence*
 - local file header
  -
  - encryption header *optional*
  - file data
  - data descriptor *optional*
 - ...

Archive Decryption *optional*
- header
- extra data record

Central Directory
- Central Directory (1 per file) *sequence*
 - header

ZIP64 EoCD *optional*
- record
- zip64 end of central directory locator

*End of Central Directory*
- end of central directory record

## Local File Header

`lfh`

<!--
name|size|type
signature|4|`.P .K 03 04`
flag|2|4: data_desc
-->

description                 | size    | comment
--------------------------- | ------- | ------------
local file header signature | 4 bytes | `0x04034b50`
version needed to extract   | 2 bytes |
general purpose bit flag    | 2 bytes | bit3 = data descriptor
compression method          | 2 bytes |
last mod file time          | 2 bytes |
last mod file date          | 2 bytes |
crc-32                      | 4 bytes |
compressed size             | 4 bytes |
uncompressed size           | 4 bytes |
file name length            | 2 bytes |
extra field length          | 2 bytes |





### data descriptor

present if `lfh.flag & 8` 

<!-- csvtable
name|size
crc|4
comp_size|4
uncomp_size|4
-->

name        | size
----------- | ----
crc         | 4
comp_size   | 4
uncomp_size | 4

## Central File Directory

<!-- csvtable
name|size|type
signature|4|`.P .K 01 02`
version|2
version_needed|2
flag|2
method|2
file_time|2
file_date|2
crc|4
comp_size|4
uncomp_size|4
name_len|2|size(filename)
extra_len|2|sze(extra_field)
com_len|2|size(file_comment)
disk_start|2
i_attrib|2
e_attriv|4
lh_offset|4
filename|?
extra_field|?
file_comment|?
-->

name           | size | type
-------------- | ---- | ------------------
signature      | 4    | `.P .K 01 02`
version        | 2    |
version_needed | 2    |
flag           | 2    |
method         | 2    |
file_time      | 2    |
file_date      | 2    |
crc            | 4    |
comp_size      | 4    |
uncomp_size    | 4    |
name_len       | 2    | size(filename)
extra_len      | 2    | sze(extra_field)
com_len        | 2    | size(file_comment)
disk_start     | 2    |
i_attrib       | 2    |
e_attriv       | 4    |
lh_offset      | 4    |
filename       | ?    |
extra_field    | ?    |
file_comment   | ?    |


# digital signature

<!--
name|size|type
signature|4|`.P .K 05 05`
size|2|
data|?
-->

name      | size | type
--------- | ---- | -------------
signature | 4    | `.P .K 05 05`
size      | 2    |
data      | ?    |


# zip64 end of central dir

<!-- csvtable
name|size|type
signature|4|`.P .K 06 06`
EoCD64 size|8
version|2
version_needed|2
disk_nb|4
cd_disk|4
disk_entries_nb|8
disk_entries|8
cd_size|8
offset|8
data_sector|?
-->

name            | size | type
--------------- | ---- | -------------
signature       | 4    | `.P .K 06 06`
EoCD64 size     | 8    |
version         | 2    |
version_needed  | 2    |
disk_nb         | 4    |
cd_disk         | 4    |
disk_entries_nb | 8    |
disk_entries    | 8    |
cd_size         | 8    |
offset          | 8    |
data_sector     | ?    |

# links

https://landave.io/2018/05/7-zip-from-uninitialized-memory-to-remote-code-execution/
