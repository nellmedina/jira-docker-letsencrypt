
### Register the Domains for SSL using Letsencrypt

Create the SSL certificates and challenges
``` bash
# create the volume to store certficates
docker volume create letsencrypt_certificates

# generate the certificates
# note that LETSENCRYPT_DOMAIN1 will become the parent certificate for the other domains
docker run --rm \
    -p 80:80 \
    -p 443:443 \
    -v letsencrypt_certificates:/etc/letsencrypt \
    -e "LETSENCRYPT_EMAIL=dummy@example.com" \
    -e "LETSENCRYPT_DOMAIN1=mario.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN2=jira.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN3=keycloak.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN4=jenkins.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN5=repo.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN6=bitbucket.nellmedina.com" \
    blacklabelops/letsencrypt install
    
# create the volume to store certficate challenges
docker volume create letsencrypt_challenges
```

Change directory to `/nginx-test` which will complete the SSL with letsencrypt
> This will integrate the nginx proxy server with two separate nginx servers secured with https.
``` bash
docker-compose up -d
```

Change directory to `/letsencrypt-autorenew` folder which will run letsencrypt each month
> This container will handshake with letsencrypt.org each month on the 15th and renew the certificate when successful.
``` bash
docker-compose run -d letsencrypt
```

Change directory to `/nginx-reload` which will reload Nginx configuration after certificates have been renewed
> Reloads Nginx configuration each month on the 15th over Docker without restarting Nginx! In order to achieve high availability!
``` bash
docker-compose up -d
```