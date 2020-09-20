International Color Consortium

http://www.color.org/specification/ICC.2-2019.pdf

https://www.argyllcms.com - tag sigs in iccV42.h

File structure

- 00+80: header
 - 00+04: profile size (size_o/s)
- 80+04: tag count (tagcount_o/s)
- `<strict min cut here>`
- 84: tag table
 - `+3*4*tagCount` [signature, offset, size]
