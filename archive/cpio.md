CPIO

https://www.mkssoftware.com/docs/man4/cpio.4.asp

# Binary form

## Structure

File: `FileS* Trailer* Padding`

FileS:
- 00+2 magic
- 02+2 device
- 04+2 inode
- 06+2 permissions
- 08+2 uid
- 0A+2 gid
- 0C+2 nlink
- 0E+2 rdevice number (0)
- 10+4 mtime[2]
- 14+2 name size (includes trailing null) - needs rounding ?
- 16+4 filesize[2]


- 1A+? `<file name>`
- ??+? `<file data>`

Trailer is a file structure of the empty file called `TRAILER!!!` (+\0)

Padding is 512 bytes