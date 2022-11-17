# 1.Port Scan
ip=10.129.210.188
`nmap -sV -sC $ip`
![e3a9fe766dfcd180ec4ecea1afa803ca.png](../_resources/e3a9fe766dfcd180ec4ecea1afa803ca.png)

# 2.Gobuster
`gobuster dir -w /usr/share/dirb/wordlists/common.txt  -u $ip`
![0b2c0c824ca0e0ff2d584ae6b5d9b0a5.png](../_resources/0b2c0c824ca0e0ff2d584ae6b5d9b0a5.png)
http://$ip/admin.php
![0e64e18e56cdbef1ef7182875e440b7b.png](../_resources/0e64e18e56cdbef1ef7182875e440b7b.png)