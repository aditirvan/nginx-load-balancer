# NGINX Load Balancer Config
### default.conf
```
upstream backend {
	server 10.130.127.167;	#node1
	server 10.130.128.35;	#node2
}

server {
	listen 80;
	server_name example.com www.example.com;

	location / {
		proxy_redirect off;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Host $http_host;
		proxy_pass http://backend;
	}
}
```
dont forget to disable SELinux
``
setsebool -P httpd_can_network_connect 1
``
## Restart Nginx
```
sudo nginx -t
sudo systemctl restart nginx
```
## Author
Adhithia Irvan Rachmawan <adhithia.irvan@gmail.com>
