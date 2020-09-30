Microsoft Cabinet File

# Docs & Tools
http://download.microsoft.com/download/4/d/a/4da14f27-b4ef-4170-a6e6-5b1ef85b1baa/[ms-cab].pdf

Tools
- Cabinet Maker `makecab.exe`
- File Expansion Utility `expand.exe`

# Format

## Structure

```
Header CFFolder+
  |        |
  |        |   <- [cut here]
  |        |
  |        +- coffCabStart -> CFData*
  |
  +- coffFiles -> CFFILE+
```	

## Header

*CFHEADER*:
- 00+4 *signature*:  `.M .S .C .F`
- 04+4 *reserved1*: set to `0`
- 08+4 *cbCabinet*: size of the file
- 0C+4 *reserved2*: set to `0`
- 10+4 *coffFiles* **absolute offset** to first CfFile netry
- 14+4 *reserved3*: set to `0`
- 18+1 *versionMinor*: set to `3` 
- 19+1 *versionMajor*: set to `1`
- 1A+2 *cFolders*: count of folders entries
- 1C+2 *cFiles*: count of files entries
- 1E+2 *flags*: `0PNR000000000000`
  - P: (*cfhdrPREV_CABINET*) The flag is set if this cabinet file is not the first in a set of cabinet files. When this bit is set, the *szCabinetPrev* and *szDiskPrev* fields are present in this *CFHEADER* structure.
  - N: (*cfhdrNEXT_CABINET*) The flag is set if this cabinet file is not the last in a set of cabinet files. When this bit is set, the *szCabinetNext* and *szDiskNext* fields are present in this *CFHEADER* structure.
  - R: (*cfhdrRESERVE_PRESENT*) The flag is set if if this cabinet file contains any reserved fields. When this bit is set, the *cbCFHeader*, *cbCFFolder*, and *cbCFData* fields are present in this *CFHEADER* structure.
- 20+2 *setID*: common ID of cabs of same set.
- 22+2 *iCabinet*: sequential number in a set


## Folder

Pointed by *coffFiles*, ordered by *iFolder*

*CFFOLDER*
- 00+4 *coffCabStart*: **absolute offset** of first data field block.
- 04+2 *cCfData*: number of data structures for this folder in this cabinet.
- 06+2 *typeCompress*:
 - `0x0000` *tcompTYPE_NONE* No compression.
 - `0x0001` *tcompTYPE_MSZIP* MSZIP compression.
 - `0x0002` *tcompTYPE_QUANTUM* Quantum compression.
 - `0x0003` *tcompTYPE_LZX* LZX compression.
- 08+? *abReserve* (optional)


## File

*CFFILE*
- 00+4 *cbFile*: uncompressed size.
- 04+4 *uoffFolderStart*: uncompressed offset of the start of this file's data.
- 08+2 *iFolder*: index of the folder that contains this file's data.
- 0A+2 *date*
- 0C+2 *time*
- 0E+2 *attribs*: `0RHS00AEU0000000`
 - R: (`_A_RDONLY`) File is read-only.
 - H: (`_A_HIDDEN`) File is hidden.
 - S: (`_A_SYSTEM`) File is a system file.
 - A: (`_A_ARCH`) File has been modified since last backup.
 - E: (`_A_EXEC`) File will be run after extraction.
 - U: (`_A_NAME_IS_UTF`) The szName field contains UTF.
- 10+? szName


## Data

*CFDATA*
- 00+4 *csum*: checksum
- 04+2 *cbData*: compressed size
- 06+2 *cbUncomp*: uncompressed size
- 08+? *abReserved*:
- ??+? *ab* compressed data


# Security Considerations

None.

## Security Considerations for Implementers

None.

## Index of Security Fields

None.
