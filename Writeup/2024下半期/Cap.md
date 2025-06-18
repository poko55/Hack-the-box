# 1.Port Scan

対象マシンのポートをスキャン
```$=10.10.10.245 ip=$ip nmap -sC -sV -p- -Pn $ip```
![a6ded0fbe1c3a6f17b93e232e82b2432.png](/_resources/a6ded0fbe1c3a6f17b93e232e82b2432.png)
上記コマンドからTCPポートが3つ開いていることを確認

`ftp $ip`
![20af9369786b56389f4721bef738e30c.png](../_resources/20af9369786b56389f4721bef738e30c.png)
ftpへのアクセスを試行したが失敗

![d6444acc60a502530c098c3b26a6736e.png](../_resources/d6444acc60a502530c098c3b26a6736e.png)ポート80のhttpにアクセスした結果アクセスに成功した

各ページを確認した所を記載

```URL「http://$ip/data/*」の数字を変更することで別ユーザに切り替えれることを確認```
URL：[http://$ip/data/1](http://10.10.10.245/data/1)
![b0d33aceded5d7508d0ab54efd8d3958.png](../_resources/b0d33aceded5d7508d0ab54efd8d3958.png)
URL:```http://ip/data/0```でダウンロードできるPCAPファイルを確認
内容を精査した結果user名/パスワードの記載を確認
![e2199c592507d49b52b4580d390ee4c5.png](../_resources/e2199c592507d49b52b4580d390ee4c5.png)
