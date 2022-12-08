# 1.Port Scan
ip=10.129.160.207
nmap -sC -sV $ip

![4cd671fbf64e0a60206bd083b22d6718.png](../_resources/4cd671fbf64e0a60206bd083b22d6718.png)

# 2.FTP Login
nmapから得た情報を使いFTPサーバにログインする。
backup.zipを確認。

ftp $ip

![0246dd1b5cd894512e6f1b007b974e5b.png](../_resources/0246dd1b5cd894512e6f1b007b974e5b.png)

# 3. Zip2john

backup.zupのhase値を出力

`zip2john backup.zip > hashes`

![4bc6747c4aff6f97108d51695c988b12.png](../_resources/4bc6747c4aff6f97108d51695c988b12.png)

John the Ripperを使いパスワードを解析

`cat hashes`

`john --wordlist=/usr/share/wordlists/rockyou.txt hashes`

![1d9b7c1bca052b9fccd0000ff47b016d.png](../_resources/1d9b7c1bca052b9fccd0000ff47b016d.png)

中身を確認
ユーザネームとパスワードを発見

cat index.php

![711c6d060e37349d300d6438d860a12c.png](../_resources/711c6d060e37349d300d6438d860a12c.png)

使用できるハッシュ形式を確認。

`hashid 2cb42f8734ea607eefed3b70af13bbd3`  

![ccfe9b2fd0886cca220012aa78c8163a.png](../_resources/ccfe9b2fd0886cca220012aa78c8163a.png)

Web site上のadminユーザのパスワードを確認

![7683f18cc4107f0a07daef542ddfde42.png](../_resources/7683f18cc4107f0a07daef542ddfde42.png)

# 4.Web site login

Web siteにログイン

![f961fa5da593059b9107e4b21a8f3c22.png](../_resources/f961fa5da593059b9107e4b21a8f3c22.png)

![e659228b8fdb3272ed3bc31d6e770665.png](../_resources/e659228b8fdb3272ed3bc31d6e770665.png)

smaple kensaku wo zissi


![fa7758357cab35ce1ce431278078ad7b.png](../_resources/fa7758357cab35ce1ce431278078ad7b.png)

![a5a624462165fca2dfa9e17430b9a72a.png](../_resources/a5a624462165fca2dfa9e17430b9a72a.png)rm