# 1.Port Scan
ip=10.129.195.240
nmap -sC -sV $ip   
![3f38fe3669d63d54b6a3f7792f435f7b.png](../_resources/3f38fe3669d63d54b6a3f7792f435f7b.png)

# 2. Gobuster
 `gobuster dir -u http://$ip/ -w /home/kali/Three/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt` 
![9648152d0b5b561ba28285a2f1314fee.png](../_resources/9648152d0b5b561ba28285a2f1314fee.png)

# 3.Login
user: **admin'#**
pass: *