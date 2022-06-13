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


- ProfileSize,4b
- PreferredCMM,4
- ProfileVersionNumber,4
- Class,4s
- ColourSpace,4s
- PCS,4s
- DateAndTime,12
  1. Year, 2bd
  1. Month, 2bd
  1. Day, 2bd
  1. Hours, 2bd
  1. Minutes, 2bd
  1. Seconds, 2bd
- Signature, 4s
- Primary Platform, 4
- Profile Flags, 4
- Device Manufacturer, 4
- Device Model, 4
- Device Attributes, 8
- Rendering Intent, 4
- PCS IlluminantX, 4
- PCS IlluminantY, 4
- PCS IlluminantZ, 4
- Profile signature, 4
- Profile ID, 16
- Reserved, 28