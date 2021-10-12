# Basic Nmap Commands

Basic Ping Scan against a network range
```
nmap -sn 192.168.0.0/24
```

TCP Scan with Default Scripts and OS detection against a network range
```
nmap -sT -sC -O 192.168.0.0/24
```

UDP Scan against a network range
```
nmap -sU 192.168.0.0/24
```

Single Port scan with Default Scripts against a single target
```
nmap -p 443 -sC 192.168.1.1
```

Nmap scan against a single target with version detection and default scripts run on the top 1000 ports that are found
```
nmap -sC -sV -oA c:\hosts\10.10.10.123-initial-scan 10.10.10.123
```

All Port Scan with output in all formats on a single host
```
nmap -p- -oA c:\hosts\192.168.1.1\Full-Port-Scan.txt 192.168.1.1
```
