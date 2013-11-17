# ReverseMe

Création de configuration reverse-proxy Nginx

```bash
# author: 111117
upstream google-v1.0-prod_backend {
	server 10.226.150.12:9001 max_fails=3 fail_timeout=30s;
	server 173.194.40.120:80 max_fails=3 fail_timeout=30s;
}
server {
	location /google-v1.0-prod{
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		rewrite /(.*) /$1 break;
		proxy_pass http://google-v1.0-prod_backend;
	}
}
```

Beta force 4, c'est une démo bac à sable pour faire une maquette !