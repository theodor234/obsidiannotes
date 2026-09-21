-add vhost to the /etc/hosts file also do not add the port 
-**use to find vhosts:** gobuster vhost -u http://inlanefreight.htb:30426 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
**-use to find hidden directories:** gobuster dir -u http://inlanefreight.htb:30426 -w /usr/share/seclists/Discovery/Web-Content/common.txt
-search the robots.txt folder
**Crawling:**
pip3 install scrapy  
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip  
unzip ReconSpider.zip

python3 ReconSpider.py http://dev.web1337.inlanefreight.htb:31170
the result is in results.json 
