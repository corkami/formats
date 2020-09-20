# iNES emulator format, standard for NES roms

https://wiki.nesdev.com/w/index.php/INES

File Structure:
`Header:16 (Trainer:512)? PRG:16384*x CHR:8192*y`

Header:
```
  0           4  5  6           A  B           F
 .N .E .S ^Z Pr Ch Fl Fl Fl Fl ZZ 00 00 00 00 00
```

- 00+4: Magic `.N .E .S ^Z`
- 04+1: Prg `x`
- 05+1: CHR
- 06+1: Flag6

```
           76543210
           ||||||||
           |||||||+- Mirroring: 0: horizontal (vertical arrangement) (CIRAM A10 = PPU A11)
           |||||||              1: vertical (horizontal arrangement) (CIRAM A10 = PPU A10)
           ||||||+-- 1: Cartridge contains battery-backed PRG RAM ($6000-7FFF) or other persistent memory
           |||||+--- 1: 512-byte trainer at $7000-$71FF (stored before PRG data)
           ||||+---- 1: Ignore mirroring control or above mirroring bit; instead provide four-screen VRAM
           ++++----- Lower nybble of mapper number
```
- 07+1: Flag7

```
           76543210
           ||||||||
           |||||||+- VS Unisystem
           ||||||+-- PlayChoice-10 (8KB of Hint Screen data stored after CHR data)
           ||||++--- If equal to 2, flags 8-15 are in NES 2.0 format
           ++++----- Upper nybble of mapper number
```
