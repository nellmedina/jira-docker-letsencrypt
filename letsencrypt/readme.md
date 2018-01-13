
#### Register the Domains for SSL using Letsencrypt

Create the volumes
``` bash
# create the certificate data
docker volume create letsencrypt_certificates

# create the certificate data
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

Run the container but command as `renewal` is used
``` bash
docker-compose run --rm letsencrypt renewal
```