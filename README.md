# Scanning
Lab 7 Vulnerabilities Analysis

## Question 1: Analyse packet1.pcap and find the flag.

<img width="940" height="420" alt="image" src="https://github.com/user-attachments/assets/1d51f46e-564c-45ef-9a7c-965712359cc2" />

<img width="767" height="148" alt="image" src="https://github.com/user-attachments/assets/973c44f9-6221-44c5-98c3-530b4ab6e2ce" />

## Question 2: Analyse packet2.pcap and ﬁnd the ﬂag.

<img width="939" height="370" alt="image" src="https://github.com/user-attachments/assets/a58d2259-b498-48f0-a30b-77c6152e63e3" />

<img width="939" height="261" alt="image" src="https://github.com/user-attachments/assets/eb5fbe2e-3735-4172-ba5c-10a3a8888735" />

## Question 3: Interpret an Nmap Output

|PORT|STATE|SERVICE|VERSION|
|----|-----|-------|-------|
|21/tcp|open|6p|vs6pd 2.3.4|
|22/tcp|open|ssh|OpenSSH 5.3p1|
|80/tcp|open|hBp|Apache 2.2.8|
|139/tcp|open||netbios-ssn|
|445/tcp|open|microso66-ds|Windows 7 Professional 7601 Service Pack 1|

1.	What can an attacker do with each port?
   
    ### •	Port 21 (FTP)
   
  	  i.	Attempt log in using any username that ends with :) and any password
  	
  	  ii.	Brute-force attacks by using tools like Hydra
  	
  	  ### •	Port 22 (SSH)
  	i.	Attempt to brute-force password to gain remote command-line access
  	•	Port 80 (HTTP)
  	
  	i.	Probe the web server for misconfigurations, directory traversal or host-based vulnerabilities
  	
  	ii.	Searches for hidden folder like /admin, /config or/backup by using tools like gobuster or dirb
  	
  	iii.	Uploads malicious file like shell.php instead of an image to allow them run command on the Windows 7 machine through the web browser
  	
  	  ### •	Port 139 and 445 (SMB)
  	
  	i.	Steal files by access unprotected shares or use stolen credentials
  	
  	ii.	Control system by using EternalBlue MS17-010 to gain a shell
  	
  	iii.	Steal passwords by sniff NTLM hashes or use Mimikatz after getting in
  	
  	iv.	Spread malware by using the machine as a jumping point to attack others

2. What vulnerabilities are likely present based on the version?
   |SERVICE|VERSION|VULNERABILITIES|
   |-------|-------|---------------|
   |vsftpd|2.3.4|Backdoor command execution that triggers a shell on port 6200 when a username ends with :)
   |OpenSSH|5.3p1|Username enumeration which allows attackers to guest valid system usernames based on server response times|
   |Apache|2.2.8|Dos and memory leaks|
   |SMB|Win 7 SP1|EternalBlue (MS17-010) that allows an unauthenticated attacker to execute code with system privilege|
   
3. Which one is the highest risk and why?
   Highest risk is port 445 (SMB) windows 7 SP1 because of the EternalBlue exploit. EternalBlue allows for Remote Code Execution (RCE) almost instantly without needing any credentials. The attacker can gained full access to the root level control over the computer and can move laterally through the rest of the network
   
4. What attack path can be built from this?
   
   i.	Use Metasploit to launch ms17_010_eternalblue exploit against port 445
   
   ii.	Use tool like Mimikatz to pull clear-text password or hashes from the memory to see if the user is and admin on other machines
   
   iii.	Use FTP or SSH to move stolen data out of the network or install permanent backdoor for future access.

5. What should be the remediation?
   
   i.	Disconnect the machine from network

   ii.	Replace the operating system with a modern and supported version like Windows 10 and above or a current Linux distribution

   iii.	Ensure MS17-010 is manually patched and the vsftpd version is updated to a non-backdoor version

   iv.	Close port 21, 139 and 445 to the public internet

   v.	Use VPN if remote access to SMB shares is required



## Question 4: Identify the OS (OS Fingerprinting) -TTL

Image 1:
<img width="776" height="272" alt="image" src="https://github.com/user-attachments/assets/30729c3e-7614-4842-80a9-561221129238" />

Answer: Linux/ Unix/ macOS/ FreeBSD

Image 2:
<img width="441" height="300" alt="image" src="https://github.com/user-attachments/assets/b4a58a81-d5be-4536-bcdb-2d2761e6abac" />

Answer: Solaris, Cisco, Juniper

Image 3:
<img width="809" height="186" alt="image" src="https://github.com/user-attachments/assets/248ff382-8271-4523-846e-a6e896d34b12" />

Answer: Windows


## Question 5: Analyse the Nessus file

<img width="565" height="552" alt="image" src="https://github.com/user-attachments/assets/37e0db9c-d6aa-4f2d-9b6f-1e6dee7453a9" />

<img width="210" height="689" alt="image" src="https://github.com/user-attachments/assets/448f6089-3210-4b48-875e-cc37af1d31d1" />


1. What is the affected Port number
   - Port 8009
     
2. What is the Aﬀected protocol
   - Apache JServe Protocol
     
3. What is the CVSS Score of vulnerability found
   - 9.8
     
4. Can you ﬁnd any exploit related to this vulnerability?
   - Metasploit
     
5. Find CVE for this vulnerability.
   - CVE-2020-1938, CVE-2020-1745



