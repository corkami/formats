# [Microsoft Compiled HTML Help .CHM](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help)

Magic: `ITSF`: "Info-Tech Storage Format"

1. download and decompress [HTML Help Workshop](https://www.microsoft.com/en-us/download/details.aspx?id=21138)
1. run `regsvr32 itcc.dll` on an admin command prompt


- `small.chm`: running HTML help workshop on a new file
- `doxygen.chm`/`.chi` (index): running Doxygen Wizard on `file.cfg` example, then open and compile the generated `index.hhp` with `hhw.exe`
