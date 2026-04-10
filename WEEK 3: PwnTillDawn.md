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

