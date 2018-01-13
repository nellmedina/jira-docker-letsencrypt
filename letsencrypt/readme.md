
#### Register the Domains

1. create volumes
``` bash
docker volume create letsencrypt_certificates

# this is required for SSL challenges
docker volume create letsencrypt_challenges
```

2. run the docker-compose file that will create SSL keys
``` bash
docker-compose up
```

3. this is running the container but command as `renewal` is used
``` bash
docker-compose run --rm letsencrypt renewal
```