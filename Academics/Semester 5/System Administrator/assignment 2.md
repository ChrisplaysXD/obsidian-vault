---
title: assignment 2
created: 2026-09-25
tags:
  - academic
  - semester-5
  - sysadmin
parent: "[[Academic MOC]]"
aliases: []
type: lecture-note
status: active
---

# assignment 2

> [!abstract] Lecture Summary
> Brief synthesis of today's lecture objectives, core theoretical theorems, or algorithms presented.

---

## 1. Core Principles & Formulations
1. Install nginx. Test it with helloworld.html
niginx is an open source software that is created to provide:
web server
	software or program that accept request via http/https and serve html and other files to a web browser
proxy server 
	proxy server is a server that sits in front of a group of client machines.
reverse proxy
	A reverse proxy is a server that sits in front of web servers and forwards client(web browser) to a web server
NGINX is frequently paired with **PHP-FPM** (for PHP applications), **Gunicorn** or **uWSGI** (for Python applications), and **PM2** (for Node.js applications) to handle dynamic content generation

For enterprise-level management and security, NGINX is often integrated with **F5 NGINX One** for observability, **NGINX Controller** for API management, and **F5 WAF** (Web Application Firewall) for Layer 7 attack protection.

NGINX load balancing method

- **Round Robin**: Distributes requests in a circular fashion; weighted variants allow faster servers to handle more traffic.
    
- **Least Connections**: Routes new requests to the server with the fewest active connections, ideal for variable request processing times.
    
- **IP Hash**: Uses the client’s IP address to hash and consistently route requests to the same backend, enabling simple session persistence.
    
- **Least Time**: Available in **NGINX Plus**, this algorithm selects the server with the lowest latency and fewest active connections.
    
- **Random**: Available in **NGINX Plus**, suitable for distributed environments where load balancers lack a full view of all requests.
PHP
	
2. Install ufw. Set to allow "Nginx HTTP"
	ufw is a program that help manage firewall rule
3. install ftp server.
	ftp is a protocol that provide a way for someone to transfer files from a server to a lcient and vice versa
4. Create an html to display your group name and the members name
	
5. Upload your html via ftp server.

6. Test your html.


---

## 2. Practical Implementation / Code
```python
# Implementation scratchpad
```

---

## 3. Key Takeaways & Review Questions
- Core takeaway 1
- Core takeaway 2

---

## Related Notes
- [[Academic MOC]]
