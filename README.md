
# WordPress Docker Compose
Original: [How To Install WordPress With Docker Compose](https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose)
> ##### Refine 
>
> - Upgrade component
> - Extract public parameter

#### Install

> Edit .env
>
> - `cp .env-example .env`
    
> Create container and obtain a certificate.
>
> 1. `cp docker-compose-step-1.yml docker-compose.yml` 
> 2. `cp ./nginx-conf/default-step-1.conf ./nginx-conf/default.conf`
> 3. `docker-compose up -d`
> 4. `docker-compose ps` *wait until service certbot exit*

> Obtaining SSL Certificates and Credentials, recreate webserver.
>
> 1. `cp docker-compose-step-2.yml docker-compose.yml` 
> 2. `docker-compose up --force-recreate --no-deps certbot`
> 3. `docker-compose stop webserver`
> 4. `curl -sSLo nginx-conf/options-ssl-nginx.conf https://raw.githubusercontent.com/certbot/certbot/master/certbot-nginx/certbot_nginx/_internal/tls_configs/options-ssl-nginx.conf`
> 5. `cp ./nginx-conf/default-step-2.conf ./nginx-conf/default.conf`
> 6. `docker-compose up -d --force-recreate --no-deps webserver`
> 4. `docker-compose ps`

> Renewing Certificates
>
> 1. `chmod +x ssl_renew.sh`
> 2. `sudo crontab -e` 
> 3. `0 12 * * * /home/sammy/wordpress/ssl_renew.sh >> /var/log/cron.log 2>&1` *add crontab task*
