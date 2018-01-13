
#### Register the Domains for SSL using Letsencrypt

Create the SSL certificates and challenges
``` bash
# create the certificate data container
docker volume create letsencrypt_certificates

# create the certificate data
# note here that DOMAIN1 will become the parent certificate for the other domains therefore points ALL certificate files to DOMAIN1 certificates.
docker run --rm \
    -p 80:80 \
    -p 443:443 \
    -v letsencrypt_certificates:/etc/letsencrypt \
    -e "LETSENCRYPT_EMAIL=dummy@example.com" \
    -e "LETSENCRYPT_DOMAIN1=mario.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN2=jira.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN3=keycloak.nellmedina.com" \
    -e "LETSENCRYPT_DOMAIN4=jenkins.nellmedina.com" \
    blacklabelops/letsencrypt install
    
# create data container for challenges before running nginx
docker volume create letsencrypt_challenges
```

Go to `blacklabelops` and run it.

Go to `letsencrypt-autorenew` folder and run this.
``` bash
docker-compose run -d letsencrypt
```

Go to `cron-nginx-reload` for automatic reload of nginx.