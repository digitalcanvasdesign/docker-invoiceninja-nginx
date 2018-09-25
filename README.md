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

