# 1. Port Scan
ip=10.129.224.213

`nmap -sV -sC $ip`
![0a2cfc8baa49e2dfb143187c0dcc464b.png](../_resources/0a2cfc8baa49e2dfb143187c0dcc464b.png)

# 2.SMBclient
`mbclient -L \\\\$1p\\`  
![65c6780292a34dbd86788f892ca3b1f4.png](../_resources/65c6780292a34dbd86788f892ca3b1f4.png)

`smbclient  \\\\10.129.224.213\\WorkShares` 
![438a88de69f6228c0fa0606d5e31a3d6.png](../_resources/438a88de69f6228c0fa0606d5e31a3d6.png)

# 3. GET flag.txt
![9bf519aa858af8eb5fb865bfe4e9c5fd.png](../_resources/9bf519aa858af8eb5fb865bfe4e9c5fd.png)