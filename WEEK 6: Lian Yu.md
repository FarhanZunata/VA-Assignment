<h2>Lian Yu Write Up - Lab Week 6</h2>
Lian Yu IP Address: 10.48.164.48
Attacker IP Address: 192.168.221.132

RECON:
1. run `nmap -sC -sV -Pn 10.48.164.48` to scanning open port.
2. port found:
   - 21 (ftp) vsftpd 3.0.2
   - 22 (ssh) OpenSSH
   - 80 (httpd)
   - 111 (rpcbind)
<img width="960" height="474" alt="nmap 6" src="https://github.com/user-attachments/assets/dd15fa11-290a-4354-907c-ad02ff8977c8" />
3. do a directory scanning to find a hidden directory
4. `gobuster dir -u http://10.48.164.48/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt`
5. found directory `/island`
<img width="960" height="474" alt="directory scanning 1" src="https://github.com/user-attachments/assets/dbe5ea41-ad70-4944-9326-5742865dc9c7" />
6. go to directory and found hidden word which is `vigilante`
 <img width="962" height="949" alt="island directory" src="https://github.com/user-attachments/assets/e4a3bfa8-671c-42bb-bc85-7b223b312e40" />
7. do a directory scanning for `/island` --> found `/2100` directory
<img width="960" height="474" alt="directory scanning 2" src="https://github.com/user-attachments/assets/a5aec695-2ad1-43cf-8b84-a813f16f2f04" />
8. go to `/2100`, but the video on page cannot play
<img width="962" height="949" alt="2100 directory" src="https://github.com/user-attachments/assets/4be82147-2426-4bef-976a-e54a22a643f8" />
9. check the source code for comment
10. found a comment says `<!-- you can avail your .ticket here but how?   -->`
<img width="962" height="949" alt="2100 source code" src="https://github.com/user-attachments/assets/acc7c09e-4b48-450f-a6b5-d0f0598e4c59" />
11. do directory scanning in `/2100` directory with `.ticket` extension
12. found a file name `green_arrow.ticket`
13. open the `.ticket` file --> 10.48.164.48/island/2100/green_arrow.ticket
<img width="962" height="949" alt="green_arrow ticket file" src="https://github.com/user-attachments/assets/109f2df5-2d2b-4d2d-b51e-8d834c84c1b7" />
14. a string shows that look like encoded string
15. use CyberChef to decode the string using Base58
<img width="962" height="949" alt="decode base58" src="https://github.com/user-attachments/assets/f15ec21e-99a3-45c9-b912-f74fad4b128f" />
16. the string is `RTy8yhBQdscX` --> after decode = `!#th3h00d`
17. the decoded string are the password for ftp login
18. the username are possible to be `vigilante` we found earlier

ENUMERATION:
1. login ftp using the username: `vigilante` and password: `!#th3h00d`
<img width="960" height="474" alt="ftp login" src="https://github.com/user-attachments/assets/71cbf950-06d3-4762-8717-f1533da07900" />
2. check the `/home` directory to see if there is other user
3. found 2 user:  `slade` and `vigilante`
<img width="960" height="474" alt="2 users" src="https://github.com/user-attachments/assets/b3b0ccbe-915c-42ee-8940-ccbfc070b1ee" />
4. list all file using `ls -la`
<img width="960" height="474" alt="get image" src="https://github.com/user-attachments/assets/f5e143d6-12f3-466f-8546-0ae0a3757447" />
5. download all the image, .other_user and .profile file using get
<img width="960" height="474" alt="get image" src="https://github.com/user-attachments/assets/c2af8dbf-a88e-47f6-88ee-8064a8228daf" />
6. open the .other_user file using `cat .other_user`
7. found a paragraph with name `Slade Wilson`
8. others name in the paragraph:
   - Captain Adeline Kane
   - Wintergreen
   - Deathstroke
   - Joseph Wilson
   - Jackal
9. check the images for embedded files using steghide and binwalk --> cannot open the image
10. check the image Leave_me_alone hex code 
<img width="960" height="474" alt="hexeditor leave me alone" src="https://github.com/user-attachments/assets/8a398db8-af6d-43f1-855e-2cbaa5b9b552" />
11. the image header are incorrect, the correct header is `89 50 4E 47 0D 0A 1A 0A`
12. Leave_me_alone image open successfully and found a `password`
<img width="845" height="475" alt="Leave_me_alone" src="https://github.com/user-attachments/assets/86995cbd-61e5-4fad-a3e3-405abf9c58e9" />
13. extract hidden data from the `aa.jpg` using the passphrase: `password` from previous image
14. found ss.zip file
<img width="960" height="474" alt="extract aa image" src="https://github.com/user-attachments/assets/5d33673c-4877-4ff1-bf22-4ca216793415" />
15. unzip ss.zip file and found 2 file which is:
      - passwd.txt
      - shado
<img width="960" height="474" alt="unzip ss file" src="https://github.com/user-attachments/assets/11c7cf71-549e-41c3-a0e4-9c268f131fa0" />
16. open both file to see the content

`passwd.txt` file
<img width="960" height="474" alt="passwd txt file" src="https://github.com/user-attachments/assets/13b16df6-29f4-4d2d-82bc-1cfc79bb214f" />

`shado` file
<img width="960" height="474" alt="shado file" src="https://github.com/user-attachments/assets/60eea7df-1c2f-473a-b860-56542c749137" />
17. in `shado` file its look like a possible password for SSH access
18. try to access SSH based on the name found in the `.other_file` paragraph
19. try access SSH: ssh slade@10.48.164.48, password: M3tahuman --> Success
<img width="960" height="474" alt="ssh" src="https://github.com/user-attachments/assets/c9654747-04d0-452b-91ae-8a969f045475" />
20. run ls to see if there is a file in home directory --> found `user.txt` file
21. open `user.txt` file and found flag --> `THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T}`
<img width="960" height="474" alt="user flag" src="https://github.com/user-attachments/assets/ddd2ed7c-208e-4e27-a418-e3401aafb1b7" />

PRIVILEGE ESCALATION:
- check which commands that cound run with current privileges
- escalate to root using sudo permissions
- sudo /usr/bin/pkexec /bin/bash and Boom!! you got the root access
- check if there is a file in the home directory
- found `root.txt` file
- open it and found root flag --> `THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}`
<img width="960" height="474" alt="root flag" src="https://github.com/user-attachments/assets/98f8ede7-f666-4356-816b-4b9e887a4bab" />




