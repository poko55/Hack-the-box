# 1.Port Scan
ip=10.129.167.249
nmap -sC -sV $ip

![ccd7ca1acd2ebc1ef3b8dc1af2bcb3a9.png](../_resources/ccd7ca1acd2ebc1ef3b8dc1af2bcb3a9.png)

# 2. Ignition.htb Connect
`curl -v http://$ip/`

![133d748f116be01ad9826854c0690c0b.png](../_resources/133d748f116be01ad9826854c0690c0b.png)


`sudo vim /etc/hosts`

![452dfa289d45e36cd182207d1ec5b7b6.png](../_resources/452dfa289d45e36cd182207d1ec5b7b6.png)
![f0eabc56056712acf4b56e53eefeae42.png](../_resources/f0eabc56056712acf4b56e53eefeae42.png)

# 3.Find Hidden page
 gobuster dir --url http://ignition.htb/ --wordlist /home/kali/Three/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt

![807980c73a5c2bc91d02806e6902e3a3.png](../_resources/807980c73a5c2bc91d02806e6902e3a3.png)

**http://ignition.htb/admin**

![a62ec36a913a8ae69d9ea54425bb0e49.png](../_resources/a62ec36a913a8ae69d9ea54425bb0e49.png)

# 4.Flag.get
![7eb34ca8751c3948649d3b76e3218a1d.png](../_resources/7eb34ca8751c3948649d3b76e3218a1d.png)

![ef85320d7f7d97cfeff8443230dd2fab.png](../_resources/ef85320d7f7d97cfeff8443230dd2fab.png)

![62f972d9f7f7d7e2a57fee635aeaea11.png](../_resources/62f972d9f7f7d7e2a57fee635aeaea11.png)





