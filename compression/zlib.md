# ZLIB

`CM:1 -> FLG:1 -> (Preset:1)? -> Data:? -> Adler:4`

<!--
macro_rules! named {
    ($CMF8:expr $FLG8:expr $($Preset32:expr)? $Data_:expr $Adler32:expr) => { ... };
}
-->

CMF (Compression Method and flags)

CM: Compression Method
- CMF:1 (usually `78`) `CM:4`, `CINFO:4`
  - CM (compression method): only deflate = 8
  - CINFO (compression info): 0-7: Window lookup size = 2^(8+compINFO). CINFO=7 => 32Kb window

FLG: Flags
- FLG:1 `FCHECK:5`, `FDICT:1`, `FLEVEL:6`
  - FCHECK (checksum): so that (256\*CMF + FLG) is divisible by 31
  - FDICT (preset dictionary)
  - FLEVEL (compression level): 0/fastest, 1/fast, 2/default, 3/max for Deflate
- PRESETDICT:4 (if FDICT is set)
- DEFLATE data:?
- adler:4

http://calmarius.net/?lang=en&page=programming%2Fzlib_deflate_quick_reference
