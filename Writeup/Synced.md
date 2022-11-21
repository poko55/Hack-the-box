# 1.Port Scan
ip=10.129.228.37
nmap -sV -sC  $ip
![85ac0168e45b11dc37f1ab2e819796c5.png](../_resources/85ac0168e45b11dc37f1ab2e819796c5.png)

# 2.Rsync

## rsync connect
`rsync --list-only $ip::public/flag.txt flag.txt`

## flag get
![d25ebfa5675b970b402df89104746a19.png](../_resources/d25ebfa5675b970b402df89104746a19.png)