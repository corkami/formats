# Microsoft Shell Link

`[MS-SHLLINK]`: Shell Link (.LNK) Binary File Format
- https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-shllink/16cb4ca1-9339-4d0c-a68d-bf1d6cc0f943
- https://github.com/libyal/libfwsi/blob/master/documentation/Windows%20Shell%20Item%20format.asciidoc


# ShellLinkHeader
- LinkTargetIDList
- Size:2
- IdList: `ItemIDList* TerminalID:2`
    - ItemIDList: `ItemIDSize:2 Data:*`
- LinkInfo


# ShellLinkHeader
- 00+4: Header Size `0x0000004C`
- 04+10: LinkCLSID `00021401-0000-0000-C000-000000000046`
- ....
