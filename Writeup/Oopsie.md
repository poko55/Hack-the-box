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

## 3 Fuzzing
## admin info
右図赤枠の箇所でファジングを実施

![d632620577c6476d0c97e392a316067d.png](../_resources/d632620577c6476d0c97e392a316067d.png)

ID=1がadminであることを確認

![c3415e527202f0309347b802d9ed8978.png](../_resources/c3415e527202f0309347b802d9ed8978.png)


## .4 Revers shell
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

