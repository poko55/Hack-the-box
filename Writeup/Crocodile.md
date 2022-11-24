# 1.Port Scan
ip=10.129.166.26
`nmap -sC -sV $ip`

![373eaefdf921c54a5dccd924bfe039c1.png](../_resources/373eaefdf921c54a5dccd924bfe039c1.png)

# 2.FTP Server Connect
`ftp $ip`

![818635f13d1dc9740e4e053b0f44a44a.png](../_resources/818635f13d1dc9740e4e053b0f44a44a.png)

# 3.Wappalyzer
![cae2705a549ca8743298e8f1ba8fece6.png](../_resources/cae2705a549ca8743298e8f1ba8fece6.png)

# 4. Sarch login
`gobuster dir --url http://$ip/ --wordlist /home/kali/Three/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt -x php,html`

![4062735233f9e221f7c10f2f2ee6e8b6.png](../_resources/4062735233f9e221f7c10f2f2ee6e8b6.png)

# 5.Flag get
http://10.129.166.26/login.php

![fe946de3776c567ac216269e843d212f.png](../_resources/fe946de3776c567ac216269e843d212f.png)