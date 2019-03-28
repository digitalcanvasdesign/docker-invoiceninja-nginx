# InvoiceNinja + Nginx + Cron Docker Bundle

[![Automated](https://img.shields.io/docker/automated/digitalcanvasdesign/invoiceninja-nginx.svg)](https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/)
[![Build](https://img.shields.io/docker/build/digitalcanvasdesign/invoiceninja-nginx.svg)](https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/)
[![Image Size](https://img.shields.io/microbadger/image-size/digitalcanvasdesign/invoiceninja-nginx.svg)](https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/)

The main container provided by [Invoice Ninja](https://github.com/invoiceninja/dockerfiles/blob/master/Dockerfile) only includes the base project. It does not provide a running cron job or web server. I prefer to run this project with all the necessary parts bundled in a single container. 

### Log mount points

Mount volume for cron and web sserver logs.

- `/var/log/ninja_cron`
- `/var/log/nginx`

### References

- We extends this base image: [https://hub.docker.com/r/invoiceninja/invoiceninja/](https://hub.docker.com/r/invoiceninja/invoiceninja/)
- [https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/](https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/)
- [https://github.com/invoiceninja/dockerfiles/tree/master/docker-compose](https://github.com/invoiceninja/dockerfiles/tree/master/docker-compose)

### Docker-compose

```yml
version: '3.7'

volumes:
  mysql_data: {}

services:
  traefik:
    image: traefik
    command: ["--docker", "--api", "--ping"]
    volumes:
    - /var/run/docker.sock:/var/run/docker.sock:ro
    ports:
    - "80:80"
    - "443:443"
    - "8080:8080"

  mysql:
    image: percona:latest
    ports:
    - "127.0.0.1:3306:3306"
    volumes:
    - mysql_data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: invoice_ninja
      MYSQL_USER: invoice_ninja
      MYSQL_PASSWORD: mypassword

  invoice:
    image: digitalcanvasdesign/invoiceninja-nginx
    build: .
    volumes:
    - ./storage:/var/www/app/storage
    - ./logs/ninja_cron:/var/log/ninja_cron
    - ./logs/nginx:/var/log/nginx
    environment:
      TRUSTED_PROXIES: '10.0.0.0/8,172.16.0.0/12,192.168.0.0/16'
      PHANTOMJS_BIN_PATH: /usr/local/bin/phantomjs
      APP_ENV: development
      APP_DEBUG: 1
      APP_URL: http://localhost
      APP_KEY: base64:WYbh/mOj2odAYpm6Hcuv1p0x+td8VYJyUqILncHo+pw=
      APP_CIPHER: AES-256-CBC
      DB_TYPE: mysql
      DB_HOST: mysql
      DB_DATABASE: invoice_ninja
      DB_USERNAME: invoice_ninja
      DB_PASSWORD: mypassword
    labels:
    - "traefik.enable=true"
    - "traefik.port=80"
    - "traefik.frontend.rule=Host: localhost"

```
