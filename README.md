- replace .env.docker with settings in this file
- uses apache2 for reverse proxy >> config located at docker/000.something.conf file


### nginx config

```
server {
    listen 80;
    server_name password.pathan.life;

    location / {
        proxy_pass http://localhost:80;  # change this to the port of the application
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### getting ssl cert using certbot
```
sudo certbot --nginx -d subdomain.domain.com
```



