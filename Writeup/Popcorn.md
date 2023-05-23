# ＃1\. Port scan

ip=10.10.10.6

sudo nmap -sC -sV $ip

![7f291095db2eb1022109dbfb2781465d.png](../_resources/7f291095db2eb1022109dbfb2781465d.png)"

# #2\. 対象HP/ディレクトリを検索

スキャンしたHPにアクセスした。

http://$ip

![08de5aeb10b8338e732eab98c7166b66.png](../_resources/08de5aeb10b8338e732eab98c7166b66.png)

gobusterでディレクトリの検索を実施した。

gobuster dir --url http://$ip/ --wordlist /usr/share/wordlists/dirb/big.txt

![14919dfee18bb3d95e522dcdb8595276.png](../_resources/14919dfee18bb3d95e522dcdb8595276.png)

/testディレクトリにアクセスを実施した。

`http://$ip/test`

![25abc6d10d9eedfd09ae575de04359fc.png](../_resources/25abc6d10d9eedfd09ae575de04359fc.png)

/torrentディレクトリにアクセスを実施した。

`http://$ip/torrent/`

# #3.対象HP内の機能を調査

![3d9698519e70efa0f133d9595b69efd4.png](../_resources/3d9698519e70efa0f133d9595b69efd4.png)

`http://10.10.10.6/rename/`

![18c1135354298402152239e97469ebeb.png](../_resources/18c1135354298402152239e97469ebeb.png)

アップロード機能を確認した。

![71afdd2f7b94fc8b62cf64ce0425df1a.png](../_resources/71afdd2f7b94fc8b62cf64ce0425df1a.png)

新規アカウントを作成した。

![b463d09ce3242c4c4dd16d1f8629d120.png](../_resources/b463d09ce3242c4c4dd16d1f8629d120.png)

ログインに成功した。

![4b3b3ba3221830dcf798d029e1c69a26.png](../_resources/4b3b3ba3221830dcf798d029e1c69a26.png)

# #4.アップロード機能について調査

reverse-shell.phpのアップロードを試行した。

![29c75550f4c89920f489609bc0877a60.png](../_resources/29c75550f4c89920f489609bc0877a60.png)

アップロードに失敗した。

torrentファイルをアップロードした。

![2a6dbc532f4711d57107af4d3e84f48e.png](../_resources/2a6dbc532f4711d57107af4d3e84f48e.png)

アップロードに成功した。

![92fe280fd0c6fe88b5483f1434ddb17c.png](../_resources/92fe280fd0c6fe88b5483f1434ddb17c.png)

burpsuiteでhttpリクエストをキャプチャーした所、content-Typeがapplication/x-phpであることを確認した。

![85c5ef7d2e10f9364bdda419245f93c4.png](../_resources/85c5ef7d2e10f9364bdda419245f93c4.png)

test.txtを試しにアップロードした結果、Contest-Typeがtext/plainになっているのでファイルの拡張子がそのままContest-Typeになることを確認した。

![90c8d59732d7514bd7dfc314a5111966.png](../_resources/90c8d59732d7514bd7dfc314a5111966.png)

jpegファイルのアップロードを試行して成功した。

![3d0aaf8750217b03115898b196e0544f.png](../_resources/3d0aaf8750217b03115898b196e0544f.png)

![8147f0a0e0bf0d7f5ddc1ceb6a0cb1ff.png](../_resources/8147f0a0e0bf0d7f5ddc1ceb6a0cb1ff.png)

先ほどアップロードしたスクリーンショットを確認した所、通信は発生していなかった。アップロードしたjpegファイルをそのまま実行していると推測する。

![791414db07a429011e408ffed142f2e2.png](../_resources/791414db07a429011e408ffed142f2e2.png)

Content-Typeをimage/jpegに変更したらリバースシェルもアップロードでき、実行できる可能性があると推測する。

repeater機能でcontent-typeを変更して送信した結果、成功した。

![7f4d68ef4c6956e3ccb3a63aed5081d0.png](../_resources/7f4d68ef4c6956e3ccb3a63aed5081d0.png)

# 5.リバースシェルを使用して対象サーバに接続する

ローカルマシンのポート1234を開けて待ち受ける

`sudo nc -lvnp 1234`

「image file Not Found」をクリック

![bce7649e4ffbcb9d6683b7457cd3c749.png](../_resources/bce7649e4ffbcb9d6683b7457cd3c749.png)

cd /home

cd george

![eb0b4e99a342a2994c037170be08b30d.png](../_resources/eb0b4e99a342a2994c037170be08b30d.png)

下記コマンドから対象サーバの種類とバージョンを確認した。

`uname -a`

![45060062274c41dae055a23d0df6a7af.png](../_resources/45060062274c41dae055a23d0df6a7af.png)

# #6.対象サーバの管理者権限を奪取する。

exploit databaseから

Linux Kernel 3.6.37 攻撃用コードを取得

![ff5a0f5ab762921e54f312c505f9fda5.png](../_resources/ff5a0f5ab762921e54f312c505f9fda5.png)

今回はduty cawと呼ばれる脆弱性を利用して攻撃する

Chatgptから

「Dirty COW」とは、Linuxカーネルの脆弱性の1つです。以下の検索結果を参考にすると、「Dirty COW」に関連する情報が見つかります。

「Dirty COW」の脆弱性は、Red Hat Enterprise Linux（RHEL）やFedoraなどのLinuxディストリビューションで報告されています\[1\]。この脆弱性により、攻撃者は特権の昇格やシステムの制御を行うことができます。

また、SELinux（Security-Enhanced Linux）のポリシーによって、攻撃可能な範囲が制限されていることも報告されていますが、Androidにも「Dirty COW」の脆弱性が存在するとされています\[2\]。トレンドマイクロは、既報告の攻撃とは異なる「Dirty COW」を利用した別の攻撃手法を確認しています。

ローカルサーバを立てる

![75bb57eec9d2b62de1541109c49773cb.png](../_resources/75bb57eec9d2b62de1541109c49773cb.png)

ローカルサーバから15704.cをダウンロード

![06b2e50269c703a0e10cadab1506cac9.png](../_resources/06b2e50269c703a0e10cadab1506cac9.png)

root権限を取得した。

![aa081156d786cd2a3cdc7924fdfe2194.png](../_resources/aa081156d786cd2a3cdc7924fdfe2194.png)

root.txtを取得した。

![4bd21729356b6a61d6dd378fdd2f6b9b.png](../_resources/4bd21729356b6a61d6dd378fdd2f6b9b.png)