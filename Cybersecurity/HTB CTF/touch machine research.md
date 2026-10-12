initial ip given:10.129.52.199
first check sudo nmap -A 10.129.52.199 to check for running process,operating system and their version
output:
![[Pasted image 20261009165258.png]]
---
what info we got from the scan:
PORT     STATE SERVICE        VERSION
135/tcp  open  msrpc?
3389/tcp open  ms-wbt-server?
5985/tcp open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
8443/tcp open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-cors: GET POST PUT OPTIONS
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Did not follow redirect to /login