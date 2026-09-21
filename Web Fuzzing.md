FIND THE DIRECTORY FIRST 
ffuf -u http://154.57.164.82:32070/webfuzzing_hidden_path/FUZZ -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt  

FIND THE FILE AFTER 
ffuf -u http://154.57.164.82:32070/webfuzzing_hidden_path/flag/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -e .php,.html,.txt,.bak,.js -v

RECURSIVE FUZZING
ffuf -u http://154.57.164.82:32071/recursive_fuzz/level1/level2/level3/FUZZ -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt -ic -e .html -recursion -recursion-depth 2

FUZZLING GET POST
	ffuf -u http://154.57.164.82:30147/get.php?x=FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt
	
ffuf -u http://154.57.164.82:30147/post.php -X POST  -H "Content-Type: application/x-www-form-urlencoded" -d "y=FUZZ" -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc 200 -v

**To get the flag:** curl http://154.57.164.67:31840/post.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "y=SUNWmc"


FUZZLING VHOSTS AND SUBDOMAINS
ffuf -w ~/Downloads/SecLists/Discovery/Web-Content/common.txt -ic -u http://fuzzing_fun.htb:port/ -H ‘Host: FUZZ.fuzzing_fun.htb’ -fc 403

gobuster dns -d inlanefreight.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt 


FUZZLING APIs
git clone https://github.com/PandaSt0rm/webfuzz_api.git
cd webfuzz_api
pip3 install -r requirements.txt
python3 api_fuzzer.py http://154.57.164.74:30205

ffuf -ic ignore comments