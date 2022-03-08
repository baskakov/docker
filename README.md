# BASK Docker and compose snippets

To help you deploy your docker instance faster

## Env

Almost all docker compose files use .env file variables. Create .env file in your docker-compose directory

```bash
APP_DB_HOST=video.bask.ws
APP_DB_DATABASE=dbname
APP_DB_USERNAME=foo
APP_DB_PASSWORD=bar
```

Then it will be automatically assigned to compose file variables, declared in docker-compose.yml

```bash
version: '3'
services:
  cleancontact:
    container_name: cleancontact
    build:
      context: .
    image: cleancontact:1
    ports:
      - "80:80"
    environment:
      APP_DB_HOST: ${APP_DB_HOST}
      APP_DB_DATABASE: ${APP_DB_DATABASE}
      APP_DB_USERNAME: ${APP_DB_USERNAME}
      APP_DB_PASSWORD: ${APP_DB_PASSWORD}
```