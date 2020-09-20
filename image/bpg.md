Better Portable Graphics, by Fabrice Bellard

https://bellard.org/bpg/

https://github.com/mirrorer/libbpg/blob/master/doc/bpg_spec.txt

# Structure

BPG File:
```
 0           4  5  6
Ma Ma Ma Ma Aa Bb Wi? He? Le? | [El? Ed?]
```
- 00+4 Magic `.B .P .G FB`
- 04+1 Ab pixel_format:3 alpha1:1 bit_depth:4
- 05+1 Bb color_space:4 extension_present:1 alpha2:1 limited_range:1 animation:1
- 06+? Wi picture_width:ue7(32)
- 0?+? He picture_height:ue7(32)
- 0?+? Le picture_data_length:ue7(32)

optional:
- El:? extension_data_length:ue7(32)
- Dd:? extension_data::ue7(32)

Extension data:

`[Ta? Tl? Td?]*`
- Ta:? extension_tag:ue7(32) : 5 = animation_control
- Tl:? extension_tag_length:ue7(32)
- Td:? extension_tag_data:ue7(32)
