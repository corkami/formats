# UTF8


# by character range

- `00000-00007F`:  0`xxxxxxx`
- `00080-0007FF`:  110`xxxxx` 10`xxxxxx`
- `00800-00FFFF`:  1110`xxxx` 10`xxxxxx` 10`xxxxxx`
- `10000-10FFFF`:  11110`xxx` 10`xxxxxx` 10`xxxxxx` 10`xxxxxx`


# by bytes sequence

1     | 2     | 3     | 4
----- | ----- | ----- | -----
00-7F |   .   |   .   |   .
C2-DF | 80-BF |   .   |   .
E0    | A0-BF | 80-BF |   .
E1-EC | 80-BF | 80-BF |   .
ED    | 80-9F | 80-BF |   .
EE-EF | 80-BF | 80-BF |   .
F0    | 90-BF | 80-BF | 80-BF
F1-F3 | 80-BF | 80-BF | 80-BF
F4    |*80-8F*| 80-BF | 80-BF

F4 is really followed by 80-8F and not 80-BF ?


# by value range

. |  .   |   .   |   .   |   .   |   .   |   .   |  .    |   .   |   .  
--| :--: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:
1 | 0-7F | C2-DF |  E0   | E1-EC |  ED   | EE-EF |  F0   | F1-F3 |  F4
2 |  .   | 80-BF | A0-BF | 80-BF | 80-9F | 80-BF | 90-BF | 80-BF |*80-8F*
3 |  .   |   .   | 80-BF | 80-BF | 80-BF | 80-BF | 80-BF | 80-BF | 80-BF
4 |  .   |   .   |   .   |   .   |   .   |   .   | 80-BF | 80-BF | 80-BF


- ASCII is literal.
- `F5`-`FF` don't exist
- `80`-`BF` can only be 2nd char.


# values

- `00`-`7F`: ASCII
- `80`-`BF`: trailing byte of multi byte. extra restrictions for `E0`, `ED`, `F0`, `F4`
- `C0`-`C1`: illegal
- `C2`-`DF`: first byte of 2-byte char.
- `E0`-`EF`: first byte of 3 byte character.
- `F0`-`F4`: first byte of 4-byte (non-BMP) character.
- `F5`-`FF`: illegal

BMP: Basic Multilingual Plane = 0000-FFFF (aka Plane 0)