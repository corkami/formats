
vector images for laser stuff

International Laser Display Association
https://www.ilda.com/resources/StandardsDocs/ILDA_IDTF14_rev011.pdf


# Structure
- sequence of sections (each section has a header)


## Section

```
00          04       07 08
.I .L .D .A Rr Rr Rr Fc Na Na Na Na Na Na Na Na

10                      18    1A 1B 1C 1D 1E 1F
Co Co Co Co Co Co Co Co Nr Nr Nb Nb To To Pn Re
```

- 00+4 ILDA
- 04+3 Reserved
- 07+1 Format Code
- 08+8 Frame or Color palette Name
- 10+8 Company Name
- 18+2 Number of Records (0 if terminator)
- 1A+2 Frame or Color palette Number
- 1C+2 Total frames
- 1E+1 Projector Number
- 1F+1 Reserved


## Format codes
- 0: # 3d coordinates with indexed color
  - 00+2 x
  - 02+2 y
  - 04+2 z
  - 06+1 status
  - 07+1 index
  
- 1: # 2d coordinates with indexed color
  - 00+2 x
  - 02+2 y
  - 04+1 status
  - 05+1 index
  
- 2: # Color palette
  - 00+1 r
  - 01+1 g
  - 02+1 b
  
- 4: # 3d coordinates with true color
  - 00+2 x
  - 02+2 y
  - 04+2 z
  - 06+1 status
  - 07+1 r
  - 08+1 g
  - 09+1 b
  
- 5: # 2d coordinates with true color
  - 00+2 x
  - 02+2 y
  - 04+1 status
  - 05+1 r
  - 06+1 g
  - 07+1 b
