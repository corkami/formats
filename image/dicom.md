# DICOM Digital Imaging and Communications in Medicine

- [specs](https://www.dicomstandard.org/current/) [File format](http://dicom.nema.org/medical/dicom/current/output/html/part10.html#chapter_7)
[Data set](http://dicom.nema.org/medical/dicom/current/output/html/part05.html#chapter_7) [Transfer syntax](https://dicomlibrary.com/dicom/transfer-syntax/)
- viewer/converter [mDicom](http://www.microdicom.com/)
- [ExifTools tags](https://sno.phy.queensu.ca/~phil/exiftool/TagNames/DICOM.html)
- Parser: [DCMTK](https://github.com/DCMTK/dcmtk)

- Magic: `DICM` at offset 128
- Terminator: none

- elements `Group:<H;Elements:<H;vr:2s;[reserved:<H];valueLen:<H?I;value:[valueLen]`. Characterised by their `<Group, Element>`
 - values long if `vr` in `OB/OD/OF/OL/OW/SQ/UC/UR/UT/UN`
 - long values:
   `Group:<H;Elements:<H;vr:2s;reserved:<H;valueLen:<I;value:[valueLen]`
 - short values: `Group:<H;Elements:<H;vr:2s;;valueLen:<H;value:[valueLen]`
 - examples
   - Group `0002` = File Metadata
   - Element `0002, 0000` = `FILE_META_INFORMATION_GROUP_LENGTH`

#### structure
 1. `preamble:128`
 1. 
`DICM`
 1. elements+

 In detail:
 1. File Meta (group `0002`) elements\*: 
  1. `0002, 0000` FILE_META_INFORMATION_GROUP_LENGTH
  1. `0002, 0001` FILE_META_INFORMATION_VERSION
  1. `0002, 0002` MEDIA_STORAGE_SOP_CLASS_UID
  1. `0002, 0003` MEDIA_STORAGE_SOP_INSTANCE_UID
  1. `0002, 0010` TRANSFER_SYNTAX_UID -> sub elements?
 1. Elements\*

 PIXEL DATA: `7fe0 0010`
