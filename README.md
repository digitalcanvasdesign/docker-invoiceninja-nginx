# InvoiceNinja + Nginx

The base container does not include a bundled in webserver, and I prefer to deploy this self hosted project bundled with nginx.

It extends this base image:

https://hub.docker.com/r/invoiceninja/invoiceninja/

https://hub.docker.com/r/digitalcanvasdesign/invoiceninja-nginx/

https://github.com/invoiceninja/dockerfiles

https://github.com/invoiceninja/dockerfiles/tree/master/docker-compose

Mount volume `/var/log/ninja_cron` for cron logs
