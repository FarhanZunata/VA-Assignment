<h2>Week 7 - File Analysis</h2>

Question 1: Analysis `packet1.pcap` and find the `flag`
- open the `packet1.pcap` file
- press `Ctrl` + `F` to search the flag
- Change the first dropdown to `string` and second dropdown to `Packet details`
- type `flag` to specify the search
- found 1 packets that have different length
<img width="960" height="1079" alt="image" src="https://github.com/user-attachments/assets/9e065c4b-11e9-4e7c-a9fb-4afc6a819593" />
- take the hexcode and decode it using Base64
<img width="962" height="1075" alt="image" src="https://github.com/user-attachments/assets/2cce5cb8-d28a-40db-b218-7dc94ccc323d" />
- the flag is `SUCTIX09s{ai_is_cool}`

Quesion 2: Analysis `packet2.pcap` and find the `flag`
- open `packet2.pcap` file
- press `Ctrl` + `F` to search the flag
- Change the first dropdown to `string` and second dropdown to `Packet details`
- type `flag` to specify the search
- found 1 FTP-DATA protocol that different with other protocol
<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/fc33cee9-9225-40e2-8bc5-8f2047ba41ac" />
- right click on the packet and select `Follow` --> `TCP Stream`
<img width="736" height="1074" alt="image" src="https://github.com/user-attachments/assets/ecd58770-0911-418a-8eeb-9ab18bc10ad9" />
- open the link given and this shows
<img width="955" height="1075" alt="image" src="https://github.com/user-attachments/assets/cd3cdddd-2f3f-4934-a63a-bb334615fa01" />

Question 3: Interpret an Nmap Output
 PORT     STATE SERVICE VERSION 
21/tcp   open  p     vs pd 2.3.4 
22/tcp   open  ssh     OpenSSH 5.3p1 
80/tcp   open  h p    Apache 2.2.8 
139/tcp  open  netbios-ssn 
445/tcp  open  microso-ds Windows 7 Professional 7601 Service Pack 1 

Questions:
1. What can an attacker do with each port?
   - port 21 (ftp): attacker can attempt to gain unauthorized access to file system. With specific version, they can trigger a hidden command shell
   - port 22 (ssh): attacker can perform brute-force attacks to guess credentials or use "user enumeration' to identify valid accounts on the system.
   - port 80 (http): attacker can look for outdated web applications to perform directory traversal or cross-site scripting (XSS) to steal data or deface the site.
   - port 445 (SMB): attacker can attempt to access shared files, steal password hashes, or execute code remotely to take over the machine.

2. What vulnerabilities are likely present based on the version?
   - vsftpd 2.3.4: this version is famous for a backdoor vulnerability (CVE-2011-2523) where entering a username ending in `:)` opens a shell for the attacker
   - OpenSSH 5.3p1: likely vulnerable to Information Disclosure and user enumeration flaws
   - Apache 2.2.8: this version end-of-life and contains numerous vulnerabilities like cross-site scripting (XSS) and denial of service (DoS).
   - Windows 7 Professional 7601 SP1: this specific OS buiild is highly vulnerable to MS17-010 (Eternal Blue), which targets the SMB protocol.

3. Which one is the highest risk and why?
   - Highest Risk: Port 445/tcp running Windows 7 Professional 7601 Service Pack 1
   - Why: because of the EternalBlue vulnerability. It allows for Remote Code Execution (RCE) with SYSTEM privileges (the highest level of control) without requiring any user interaction or valid login credentials.

4. What attack path can be built from this?
   - Reconnaissance: the attacker uses Nmap to identify that the target is and unpatched Windows 7 system.
   - Exploitation: attacker uses an exploit framework (like Metasploit) to launch `ms17_010_eternalblue` attack against port 445
   - Privilege Escalation: Upon success, the attacker automatically gains SYSTEM-level access, bypassing all local security.
   - Post-Exploitation: attacker can then dump administrator passwords from memory to move laterally to other computers on the network.

  5. What should be the remediation?
     - Immediate Patching: Install the MS17-010 security update from Microsoft to close the EternalBlue hole
     - Disable Legacy Protocols: Disbale SMBv1 on all systems, as it is an outdated and insecure protocol
     - Service Updates: Upgrade `vsftpd`, `OpenSSH`, and `Apache` to their latest stable versions to remove version-specific backdoors and flaws
     - OS Upgrade: Since Windows 7 no longer supported by Microsoft, the system should be upgraded to a modern, supported operating system like Windows 10 or 11.

Question 4: Identify the OS (OS Fingerprinting) - TTL

Image 1:
<img width="540" height="192" alt="image" src="https://github.com/user-attachments/assets/faecd1ef-976d-48cf-a20f-0a4f70234e70" />
Answer: Linux

Image 2:
<img width="308" height="204" alt="image" src="https://github.com/user-attachments/assets/d557bdfa-078b-42d2-85b0-1dc77598b904" />
Answer: Network Device (Cisco Router/Solaris)

Image 3:
<img width="553" height="130" alt="image" src="https://github.com/user-attachments/assets/aa97e656-3365-4966-a1bc-67416c6d7437" />
Answer: Windows

Question 5: Analyse the Nessus file
