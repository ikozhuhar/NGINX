## NGINX

Пример конфигурации для проксирования запросов на бэкенд-сервер:

```ruby
server {
    listen 80;
    server_name your-domain.com;  # или IP-адрес сервера
	
    #listen 443 ssl;
    #server_name your-domain.com;

    #ssl_certificate /path/to/cert.pem;
    #ssl_certificate_key /path/to/key.pem

    location / {
        proxy_pass http://localhost:3000;  # адрес и порт вашего бэкенд-сервера
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Если вам нужно проксировать несколько сервисов, можно использовать разные location или поддомены. 

```ruby
server {
    listen 80;
    server_name api.your-domain.com;

    location / {
        proxy_pass http://localhost:8080;
        # ... proxy_set_header
    }
}

server {
    listen 80;
    server_name app.your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
        # ... proxy_set_header
    }
}
```
