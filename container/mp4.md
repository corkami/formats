# MP4 / "QuickTime" / ISO 14496-1 Media Format / Atom/Box format

docs:
- http://standards.iso.org/ittf/PubliclyAvailableStandards/c061988_ISO_IEC_14496-12_2012.zip
- [ISO Common Encryption EME Stream Format and Initialization Data](https://dvcs.w3.org/hg/html-media/raw-file/ff10d356cc07/encrypted-media/cenc-format.html)
- http://mp4ra.org/#/atoms
- https://developer.apple.com/library/archive/documentation/QuickTime/QTFF/QTFFChap1/qtff1.html

tools:
- [Atomic Parsley](https://sourceforge.net/projects/atomicparsley/)
  - [Atoms, Boxes, Parents, Children & hex (oh my)](http://atomicparsley.sourceforge.net/mpeg-4files.html)
- [Bento4 MP4 & DASH](https://www.bento4.com/)
 - [Source](https://github.com/axiomatic-systems/Bento4)

file types:
- mp4
- quick time
- heic
- jpeg2000


# structure

No magic (!). Pure sequence of chunks called atom and boxes:
Atom contain data, Boxes can contain other atoms.
They follow the same structure.

- standard case: `ss ss ss ss` `tt tt tt tt` `dd dd .. .. dd`: size = len(size + type + data) => smallest size is 8 (see `wide` atoms)
- exceptions:
 - null size: `00 00 00 00` `tt tt tt tt` `dd dd .. .. ..`: until end of file
 - 64 bit size: `00 00 00 01` `tt tt tt tt` `ee ee ee ee ee ee ee ee` `dd dd .. ..`: extended_size = len(size + type + extended_size + data)

Special cases:
- `wide`/`free`/`skip` atom:

  A placeholder that will be put before an atom/box in case it needs to extend
  its size from 32b to 64b without relocating anything.

  before: (size on 32b)
  ```
  00 00 00 08 .w .i .d .e ss ss ss ss tt tt tt tt dd dd .. ..
  ```

  after (size on 64b)
  ```
  00 00 00 00 tt tt tt tt ee ee ee ee ee ee ee ee dd dd .. ..
  ```
  (no relocation needed)

- the `stco`/`co64` atoms contain **absolute** offsets
  pointing to the `mdat` data that *must* be correct.

  The atom `stco` (for 32 bits, or `co64` for 64 bits offsets) is a list of
  **absolute** offset (it stands for 'Sample Table - Chunk offsets') of the
  `mdat` data.

  If the `mdat` atom is moved, then updating these offsets is **required**,
  but at least it means that adding any extra chunk just implies locating offsets table,
  and applying a delta to each entry, with no other requirement.
