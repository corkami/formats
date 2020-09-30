Adobe Photoshop (incomplete file but good enough to understand how to abuse it)

Extension: `.PSD`

Large Document Format: `.PSB`

https://www.adobe.com/devnet-apps/photoshop/fileformatashtml

Big Endian.


# Structure

`Header ColModeData Resources LayersMasks ImageData`


## Header

- `00+4`: signature `8BPS`
- `04+2`: `version` 1 = PSD, 2 = PSB
- `06+6`: `reserved` - must be zero
- `0C+2`: channel counts - 1-56
- `0E+4`: height (1-30_000 PSB: 300_000)
- `12+4`: width (1-30_000 PSB: 300_000)
- `16+2`: depth 1,8,16,32
- `18+2`: color mode
 - `0`: bitmap
 - `1`: grayscale
 - `2`: indexed
 - `3`: RGB
 - `4`: CMYK
 - `7`: Multichannel
 - `8`: Duotone
 - `9`: Lab
- `1a`

## Color Mode Data

Always at offset `0x1a`.

Data only present in indexed and duotone. Set to zero for other formats.

- `00+4`: length of the data
- `04+?`: color data


## Image Resources

Present at `0x1E` if no data

- `00+4`: length of the data
- `04+?`: Image Resource Blocks

Image Resource Block
- `00+4`: signature `8BIM`
- `04+2`: UIDs
- `06+?`: Name: Pascal string, 2-padded
- `+4` size of resource
- `+?` resource data - 2-padded
