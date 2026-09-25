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

NGINX load balancing
	

2. Install ufw. Set to allow "Nginx HTTP"
	ufw is a program that help manage firewall rule
3. install ftp server.
	ftp is a protocol that provide a way for someone to transfer files from a server to a lcient and vice versa
4. Create an html to display your group name and the members name
	
5. Upload your html via ftp server.

6. Test your html.
