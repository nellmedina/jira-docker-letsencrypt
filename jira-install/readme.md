#### Install Jira with Docker Compose

Set the default environment variables that will be used by Docker Compose.

```bash
source defaultHttps.env
```

You can override password variables.
```bash
$ export JIRA_DB_USERNAME=yourusername
$ export JIRA_DB_PASSWORD=yourdbpassword
$ export JIRA_TIME_ZONE=Europe/Berlin
$ export JIRA_DOMAIN_NAME=localhost
```

Start it up!
```bash
docker-compose up -d
```

> Jira will be accessible on the set $JIRA_DOMAIN_NAME.