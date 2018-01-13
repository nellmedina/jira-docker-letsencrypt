
#### Register the Domains

Create the volumes
``` bash
docker volume create letsencrypt_certificates

# this is required for SSL challenges
docker volume create letsencrypt_challenges
```

Run the docker-compose file that will create SSL keys
``` bash
docker-compose up
```

Run the container but command as `renewal` is used
``` bash
docker-compose run --rm letsencrypt renewal
```