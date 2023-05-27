# ＃1\. Port scan

ip=10.10.10.6

sudo nmap -sC -sV $ip

![7f291095db2eb1022109dbfb2781465d.png](../_resources/7f291095db2eb1022109dbfb2781465d.png)"

tcpポート22番とtcpポート80番が開放されている事を確認した。

# #2\. 対象HP/ディレクトリを検索

開放されているtcpポート80番を調査するために当該ポートにプラウザ上からアクセスした。

http://$ip

その結果下記画面が表示された。

![08de5aeb10b8338e732eab98c7166b66.png](../_resources/08de5aeb10b8338e732eab98c7166b66.png)

Webサイト上のディレクトリ構造が不明な為、gobusterでディレクトリの列挙を実施した。

gobuster dir --url http://$ip/ --wordlist /usr/share/wordlists/dirb/big.txt

![14919dfee18bb3d95e522dcdb8595276.png](../_resources/14919dfee18bb3d95e522dcdb8595276.png)

その結果「/index」「/rename」「/test」「torrent」ディレクトリにアクセスできることを確認した。

/testディレクトリを詳細に調査する為プラウザから/testディレクトリにアクセスした。

その結果、サーバ情報を取得することに成功した。

`http://$ip/test`

![25abc6d10d9eedfd09ae575de04359fc.png](../_resources/25abc6d10d9eedfd09ae575de04359fc.png)

上記Webページからphpがサーバ上で実行できると推測した。

# #3.対象HP内の機能を調査

/torrentディレクトリを詳細に調査するためにブラウザ上でアクセスした。

`http://$ip/torrent/`

アップロード画面を示唆するリンクを発見した。

![3d9698519e70efa0f133d9595b69efd4.png](../_resources/3d9698519e70efa0f133d9595b69efd4.png)

アップロード画面にアクセスを試行した結果、ログイン画面に遷移した。

![71afdd2f7b94fc8b62cf64ce0425df1a.png](../_resources/71afdd2f7b94fc8b62cf64ce0425df1a.png)

「Sign up」から新規アカウントを作成できるかを試行した。

![23d764eeb8cc4159bb42b22c8a6ed73d.png](../_resources/23d764eeb8cc4159bb42b22c8a6ed73d.png)

上記画面でユーザ情報を入力した結果、新規アカウントの作成に成功した。

作成した新規アカウントを使用した結果、ログインに成功した。

![4b3b3ba3221830dcf798d029e1c69a26.png](../_resources/4b3b3ba3221830dcf798d029e1c69a26.png)

# #4.アップロード機能について調査

testディレクトリでphpがサーバ上で実行できる事を確認したので

php-reverse-shell.phpのアップロードを試行したが失敗した。

![29c75550f4c89920f489609bc0877a60.png](../_resources/29c75550f4c89920f489609bc0877a60.png)

上記の結果、ファイルの種別を確認していると推測されるためテスト用のtorrentファイルをアップロードした。

![2a6dbc532f4711d57107af4d3e84f48e.png](../_resources/2a6dbc532f4711d57107af4d3e84f48e.png)

その結果、アップロードに成功した。

![28f1fec18c1e38fdb74f91d91f171a14.png](../_resources/28f1fec18c1e38fdb74f91d91f171a14.png)

アップロードしたテスト用torrentファイルをWebページ内で確認した結果、下記ページに遷移した。

![92fe280fd0c6fe88b5483f1434ddb17c.png](../_resources/92fe280fd0c6fe88b5483f1434ddb17c.png)

Edit this torrentを押下した結果スクリーンショットをアップロードできる機能を発見した。

![8ca1857dd08c2f59b29e415c37769317.png](../_resources/8ca1857dd08c2f59b29e415c37769317.png)

スクリーンショットのアップロード機能をさらに調査するためにhttpリクエストをキャプチャーした。

reverse-shell-php3.phpをアップロードを試行したが失敗した。

burpsuiteでhttpリクエストをキャプチャーした所、content-Typeがapplication/x-phpであることを確認した。

![85c5ef7d2e10f9364bdda419245f93c4.png](../_resources/85c5ef7d2e10f9364bdda419245f93c4.png)

![102b046149bfe05310b8147c380cc18d.png](../_resources/102b046149bfe05310b8147c380cc18d.png)

test.txtを試しにアップロードした結果、試行したが失敗した。Contest-Typeがtext/plainになっているのでファイルの拡張子がそのままContest-Typeになると推測した。

![90c8d59732d7514bd7dfc314a5111966.png](../_resources/90c8d59732d7514bd7dfc314a5111966.png)

![e79489df34f82eba0a94d914e8533efa.png](../_resources/e79489df34f82eba0a94d914e8533efa.png)

jpegファイルのアップロードを試行して成功した。

![3d0aaf8750217b03115898b196e0544f.png](../_resources/3d0aaf8750217b03115898b196e0544f.png)

![8147f0a0e0bf0d7f5ddc1ceb6a0cb1ff.png](../_resources/8147f0a0e0bf0d7f5ddc1ceb6a0cb1ff.png)

先ほどアップロードしたスクリーンショットを確認した所、通信は発生していなかった。アップロードしたjpegファイルをWebページ上でそのまま実行していると推測した。

![791414db07a429011e408ffed142f2e2.png](../_resources/791414db07a429011e408ffed142f2e2.png)

Content-Typeをimage/jpegに変更したらリバースシェルもアップロードでき、実行できる可能性があると推測した。

php-reverse-shellをアップロードするhttpリクエストをrepeaterで改変して送信した結果、アップロードに成功した。

![7f4d68ef4c6956e3ccb3a63aed5081d0.png](../_resources/7f4d68ef4c6956e3ccb3a63aed5081d0.png)

# 5.リバースシェルを使用して対象サーバに接続する

ローカルマシンのポート1234を開けて待ち受ける

`sudo nc -lvnp 1234`

「image file Not Found」をクリックして、リバースシェルの実行に成功した。

![bce7649e4ffbcb9d6683b7457cd3c749.png](../_resources/bce7649e4ffbcb9d6683b7457cd3c749.png)

cd /home

cd george

![eb0b4e99a342a2994c037170be08b30d.png](../_resources/eb0b4e99a342a2994c037170be08b30d.png)

ユーザアカウントの/homディレクトリを検索した結果user.txtを確認した。

下記コマンドから対象サーバの種類とバージョンを確認した。

`uname -a`

対象サーバのKernelバージョンが2.6.31であることを確認した。

![45060062274c41dae055a23d0df6a7af.png](../_resources/45060062274c41dae055a23d0df6a7af.png)

# #6.対象サーバの管理者権限を奪取する。

exploit databaseからLinux Kernel 2.6.31用コードを検索した結果、

Linux Kernel 2.6.37 攻撃用コードである15704.cを取得した。

![110dda16a300522c2bc81536e30a9bfc.png](../_resources/110dda16a300522c2bc81536e30a9bfc.png)

対象のサーバから15704.cをダウンロードさせるためにローカルサーバを立てた。

![75bb57eec9d2b62de1541109c49773cb.png](../_resources/75bb57eec9d2b62de1541109c49773cb.png)

wgetコマンドを使用して15704.cをダウンロードできるかを試行した。

結果、ローカルサーバから15704.cをダウンロードさせて対象のサーバ上に保存させることに成功した。

![06b2e50269c703a0e10cadab1506cac9.png](../_resources/06b2e50269c703a0e10cadab1506cac9.png)

gccコマンドを使用して15704.cをコンパイルさせることで15704という実行ファイル生成した。

15704実行ファイルを実行させ、root権限を取得した。

![9665bcc6874fbe89d74267c3bac7809a.png](../_resources/9665bcc6874fbe89d74267c3bac7809a.png)

root.txtを取得した。

![4bd21729356b6a61d6dd378fdd2f6b9b.png](../_resources/4bd21729356b6a61d6dd378fdd2f6b9b.png)