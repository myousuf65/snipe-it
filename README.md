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


### .htaccess file config for cpanel

```
RewriteEngine On

# Redirect all traffic to port 3000
RewriteRule ^(.*)$ http://ip_address:3000/$1 [P,L]

# BEGIN cPanel-generated php ini directives, do not edit
# Manual editing of this file may result in unexpected behavior.
# To make changes to this file, use the cPanel MultiPHP INI Editor (Home >> Software >> MultiPHP INI Editor)
# For more information, read our documentation (https://go.cpanel.net/EA4ModifyINI)
<IfModule php8_module>
   php_flag display_errors on
   php_value max_execution_time 90
   php_value max_input_time 180
   php_value max_input_vars 2000
   php_value memory_limit 2048M
   php_value post_max_size 32M
   php_value session.gc_maxlifetime 2880
   php_value session.save_path "/var/cpanel/php/sessions/ea-php81"
   php_value upload_max_filesize 128M
   php_flag zlib.output_compression Off
</IfModule>
<IfModule lsapi_module>
   php_flag display_errors on
   php_value max_execution_time 90
   php_value max_input_time 180
   php_value max_input_vars 2000
   php_value memory_limit 2048M
   php_value post_max_size 32M
   php_value session.gc_maxlifetime 2880
   php_value session.save_path "/var/cpanel/php/sessions/ea-php81"
   php_value upload_max_filesize 128M
   php_flag zlib.output_compression Off
</IfModule>
# END cPanel-generated php ini directives, do not edit

# php -- BEGIN cPanel-generated handler, do not edit
# Set the “ea-php81” package as the default “PHP” programming language.
<IfModule mime_module>
  AddHandler application/x-httpd-ea-php81 .php .php8 .phtml
</IfModule>
# php -- END cPanel-generated handler, do not edit
```


