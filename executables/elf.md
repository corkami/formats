# Executable and Linkable Format

Note: Things like 14+4/28+8 are 32b & 64b.

Structure:
the file starts with *File Header*,
which points to *Program Header table* and 
*Section Header Table*.

## File Header

- 00+10 *e_ident*
 - 00+4 *EI_MAG0*    `7F .E .L .F`
 - 04+1 *EI_CLASS*   `1`:32 / `2`:64
 - 05+1 *EI_DATA*    `1`:little `2`:big
 - 06+1 *EI_VERSION* `1`
 - 07+1 *EI_OSABI*   operating system ABI - often set to `0` ?
   - `00` System V
   - `01` HP-UX
   - `02` NetBSD
   - `03` Linux
   - `04` GNU Hurd
   - `06` Solaris
   - `07` AIX
   - `08` IRIX
   - `09` FreeBSD
   - `0a` Tru64
   - `0b` Novell Modesto
   - `0c` OpenBSD
   - `0d` OpenVMS
   - `0e` NonStop Kernel
   - `0f` AROS
   - `10` Fenix OS
   - `11` CloudABI
   - `12` Stratus Technologies OpenVOS

 - 08+1 *EI_ABIVERSION* further ABI info.
 - 09+7 *EI_PAD* unused

- 10+2 *e_type* object file type.
 - `0000` *ET_NONE*
 - `0001` *ET_REL*
 - `0002` *ET_EXEC*
 - `0003` *ET_DYN*
 - `0004` *ET_CORE*
 - `fe00` *ET_LOOS*
 - `feff` *ET_HIOS*
 - `ff00` *ET_LOPROC*
 - `ffff` *ET_HIPROC*

- 12+2 *e_machine* instruction set
 - `00` No specific instruction set
 - `01` AT&T WE 32100
 - `02` SPARC
 - `03` x86
 - `04` Motorola 68000 (M68k)
 - `05` Motorola 88000 (M88k)
 - `06` Intel MCU
 - `07` Intel 80860
 - `08` MIPS
 - `09` IBM_System/370
 - `0a` MIPS RS3000 Little-endian
 - `0b`-`0d`	Reserved for future use
 - `0e` Hewlett-Packard PA-RISC
 - `0f` Reserved for future use
 - `13` Intel 80960
 - `14` PowerPC
 - `15` PowerPC (64-bit)
 - `16` S390, including S390x
 - `28` ARM (up to ARMv7/Aarch32)
 - `2a` SuperH
 - `32` IA-64
 - `3e` amd64
 - `8c` TMS320C6000 Family
 - `b7` ARM 64-bits (ARMv8/Aarch64)
 - `f3` RISC-V

- 14+4 *e_version* set to `1`

- 18+4/18+8 *e_entry*		memory adress of the entry point
- 1c+4/20+8 *e_phoff*		offset of the Program Header table - usually right after the file header at `0x34`/`0x40`
- 20+4/28+8 *e_shoff*		offset of the Section Header table
- 24+4/30+4 *e_flags*		depends on architecture
- 28+2/34+2 *e_ehsize* 		size of this header - typically `52`/`64`
- 2a+2/36+2 *e_phentsize*	size of a PH table entry
- 2c+2/38+2 *e_phnum*		number of entries in PH table
- 2e+2/3a+2 *e_shentsize*	size of a SH table entry
- 30+2/3c+2 *e_shnum*		number of entries in SH table
- 32+2/3e+2 *e_shstrndx*	index in SH table with section names
- 34/40 (end)


## Program header

- 00+4 p_type:	Identifies the type of the segment.
 - `00000000` *PT_NULL*		Program header table entry unused
 - `00000001` *PT_LOAD*		Loadable segment
 - `00000002` *PT_DYNAMIC*	Dynamic linking information
 - `00000003` *PT_INTERP*	Interpreter information
 - `00000004` *PT_NOTE*		Auxiliary information
 - `00000005` *PT_SHLIB*	reserved
 - `00000006` *PT_PHDR*		segment containing Program HeaDeR table itself
 - `00000007` *PT_TLS*		Thread-Local Storage template
 - `60000000` *PT_LOOS* - `6FFFFFFF` *PT_HIOS*
 - `70000000` *PT_LOPROC* - `7FFFFFFF` *PT_HIPROC*

   *PT_LOOS* to *PT_HIOS* (*PT_LOPROC* to *PT_HIPROC*) is an inclusive reserved ranges for operating system (processor) specific semantics.

- 04+0/04+4	*p_flags*	Segment-dependent flags (position for 64-bit structure).
- 04+4/08+8	*p_offset*	Offset of the segment in the file image.
- 08+4/10+8	*p_vaddr*	Virtual address of the segment in memory.
- 0C+4/18+8	*p_paddr*	On systems where physical address is relevant, reserved for segment's physical address.
- 10+4/20+8	*p_filesz*	Size in bytes of the segment in the file image. May be 0.
- 14+4/28+8	*p_memsz*	Size in bytes of the segment in memory. May be 0.
- 18+4/30+0	*p_flags*	Segment-dependent flags (position for 32-bit structure).
- 1C+4/30+8	*p_align*	0 and 1 specify no alignment. Otherwise should be a positive, integral power of 2, with p_vaddr equating p_offset modulus p_align.
- 20/38		End of Program Header (size)


## Section header

- 00+4 *sh_name* An offset to a string in the .shstrtab section that represents the name of this section.
- 04+4 *sh_type* Identifies the type of this header.
 - `00000000` *SHT_NULL*			Section header table entry unused
 - `00000001` *SHT_PROGBITS*		Program data
 - `00000002` *SHT_SYMTAB*			Symbol table
 - `00000003` *SHT_STRTAB*			String table
 - `00000004` *SHT_RELA*			Relocation entries with addends
 - `00000005` *SHT_HASH*			Symbol hash table
 - `00000006` *SHT_DYNAMIC*			Dynamic linking information
 - `00000007` *SHT_NOTE*			Notes
 - `00000008` *SHT_NOBITS*			Program space with no data (bss)
 - `00000009` *SHT_REL*				Relocation entries, no addends
 - `0000000A` *SHT_SHLIB*			Reserved
 - `0000000B` *SHT_DYNSYM*			Dynamic linker symbol table
 - `0000000E` *SHT_INIT_ARRAY*		Array of constructors
 - `0000000F` *SHT_FINI_ARRAY*		Array of destructors
 - `00000010` *SHT_PREINIT_ARRAY*	Array of pre-constructors
 - `00000011` *SHT_GROUP*			Section group
 - `00000012` *SHT_SYMTAB_SHNDX*	Extended section indices
 - `00000013` *SHT_NUM*				Number of defined types.
 - `60000000` *SHT_LOOS*			Start OS-specific.
- 08+4/08+8 *sh_flags*	Identifies the attributes of the section.
 - `00000001` *SHF_WRITE*				Writable
 - `00000002` *SHF_ALLOC*				Occupies memory during execution
 - `00000004` *SHF_EXECINSTR*			Executable
 - `00000010` *SHF_MERGE*				Might be merged
 - `00000020` *SHF_STRINGS*				Contains null-terminated strings
 - `00000040` *SHF_INFO_LINK*			'sh_info' contains SHT index
 - `00000080` *SHF_LINK_ORDER*			Preserve order after combining
 - `00000100` *SHF_OS_NONCONFORMING*	Non-standard OS specific handling required
 - `00000200` *SHF_GROUP*				Section is member of a group
 - `00000400` *SHF_TLS*					Section hold thread-local data
 - `0ff00000` *SHF_MASKOS*				OS-specific
 - `f0000000` *SHF_MASKPROC*			Processor-specific
 - `04000000` *SHF_ORDERED*				Special ordering requirement (Solaris)
 - `08000000` *SHF_EXCLUDE*				Section is excluded unless referenced or allocated (Solaris)
- 0C+4/10+8 *sh_addr*	 	Virtual address of the section in memory, for sections that are loaded.
- 10+4/18+8 *sh_offset* 	Offset of the section in the file image.
- 14+4/20+8 *sh_size*		Size in bytes of the section in the file image. May be 0.
- 18+4/28+4 *sh_link*		Contains the section index of an associated section. This field is used for several purposes, depending on the type of section.
- 1C+4/2C+4 *sh_info*		Contains extra information about the section. This field is used for several purposes, depending on the type of section.
- 20+4/30+8 *sh_addralign*  Contains the required alignment of the section. This field must be a power of two.
- 24+4/38+8 *sh_entsize*	Contains the size, in bytes, of each entry, for sections that contain fixed-size entries. Otherwise, this field contains zero.
- 28/40		End of Section Header (size)
