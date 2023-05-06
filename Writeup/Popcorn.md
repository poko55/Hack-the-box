# 1. Port scan
ip=10.10.10.6

sudo nmap -sC -sV $ip

![7f291095db2eb1022109dbfb2781465d.png](../_resources/7f291095db2eb1022109dbfb2781465d.png)

スキャンしたHPにアクセス


http://$ip

![08de5aeb10b8338e732eab98c7166b66.png](../_resources/08de5aeb10b8338e732eab98c7166b66.png)

gobusterでディレクトリを検索

gobuster dir --url http://$ip/ --wordlist /usr/share/wordlists/dirb/big.txt

![14919dfee18bb3d95e522dcdb8595276.png](../_resources/14919dfee18bb3d95e522dcdb8595276.png)

/testディレクトリにアクセス



`http://$ip/test`


![25abc6d10d9eedfd09ae575de04359fc.png](../_resources/25abc6d10d9eedfd09ae575de04359fc.png)

/torrentディレクトリにアクセス

`http://$ip/torrent/`

![3d9698519e70efa0f133d9595b69efd4.png](../_resources/3d9698519e70efa0f133d9595b69efd4.png)

`http://10.10.10.6/rename/`

![18c1135354298402152239e97469ebeb.png](../_resources/18c1135354298402152239e97469ebeb.png)

アップロード機能を確認

![71afdd2f7b94fc8b62cf64ce0425df1a.png](../_resources/71afdd2f7b94fc8b62cf64ce0425df1a.png)

新規アカウントを作成

![b463d09ce3242c4c4dd16d1f8629d120.png](../_resources/b463d09ce3242c4c4dd16d1f8629d120.png)

ログイン成功

![4b3b3ba3221830dcf798d029e1c69a26.png](../_resources/4b3b3ba3221830dcf798d029e1c69a26.png)


reverse-shellをアップロード

![29c75550f4c89920f489609bc0877a60.png](../_resources/29c75550f4c89920f489609bc0877a60.png)

アップロード失敗

torrentファイルをアップロード

![2a6dbc532f4711d57107af4d3e84f48e.png](../_resources/2a6dbc532f4711d57107af4d3e84f48e.png)

アップロード成功

![92fe280fd0c6fe88b5483f1434ddb17c.png](../_resources/92fe280fd0c6fe88b5483f1434ddb17c.png)



burpsuiteでパケットを受信

![1ddc84223a85b959ac882b233d93c3ef.png](../_resources/1ddc84223a85b959ac882b233d93c3ef.png)

repeater昨日でcontent-typeを変更して送信

![7f4d68ef4c6956e3ccb3a63aed5081d0.png](../_resources/7f4d68ef4c6956e3ccb3a63aed5081d0.png)

`sudo nc -lvnp 1234`

「image file Not Found」をクリック

![bce7649e4ffbcb9d6683b7457cd3c749.png](../_resources/bce7649e4ffbcb9d6683b7457cd3c749.png)

cd /home

cd george

![eb0b4e99a342a2994c037170be08b30d.png](../_resources/eb0b4e99a342a2994c037170be08b30d.png)

exploit databaseから

Linux Kernel 3.6.37 攻撃用コードを取得

![ff5a0f5ab762921e54f312c505f9fda5.png](../_resources/ff5a0f5ab762921e54f312c505f9fda5.png)

ローカルサーバを立てる

![75bb57eec9d2b62de1541109c49773cb.png](../_resources/75bb57eec9d2b62de1541109c49773cb.png)

ローカルサーバから15705.cをダウンロード

![06b2e50269c703a0e10cadab1506cac9.png](../_resources/06b2e50269c703a0e10cadab1506cac9.png)

root権限を取得

![aa081156d786cd2a3cdc7924fdfe2194.png](../_resources/aa081156d786cd2a3cdc7924fdfe2194.png)

root.txtを取得

![4bd21729356b6a61d6dd378fdd2f6b9b.png](../_resources/4bd21729356b6a61d6dd378fdd2f6b9b.png)


