# 1.Port Scan
ip=10.129.170.12

`nmap -sC -sV -Pn $ip`

![b989dca31c40ecce876db60620e9d171.png](../_resources/b989dca31c40ecce876db60620e9d171.png)

# 2.Smbclient Directory Search

`smbclient -L \\\\$ip\\ -U Administrator`

![d75cfb911650c84ca940a2f73e4f4d23.png](../_resources/d75cfb911650c84ca940a2f73e4f4d23.png)
## Flag Get
`smbclient  \\\\$ip\\C$ -U Administrator`

![67a8f48cbe86f1d02eb5e4ae98e97fb9.png](../_resources/67a8f48cbe86f1d02eb5e4ae98e97fb9.png)



