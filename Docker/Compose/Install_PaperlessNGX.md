This is my version of the docker-compose file of `paperlessngx` that works on an `oracle cloud instance`

## Docker-Compose

> [!warning] Change Me!
> - __Webserver__: Ports (the ports where you want paperless to be)
> - __Volumes__: The volumes where the data is stored on your device 
> - __Super-Admin__:
> 	- PAPERLESS_ADMIN_USER: 
> 	- PAPERLESS_ADMIN_PASSWORD: 
> 	 (your desired admin login data | used for first login)
> - __Domain__:
> 	- PAPERLESS_URL: 
> 	- PAPERLESS_CSRF_TRUSTED_ORIGINS: 
> 	(from where you gonna access paperless)
> - __UID & GID__:
> 	- USERMAP_UID: 
> 	- USERMAP_GID:
> 	(the user and group id how paperless should run)


```yaml
version: "3.9"
services:
  redis:
    image: redis
    container_name: PaperlessNGX-REDIS
    restart: on-failure:5
    volumes:
      - /home/ubuntu/docker/dockercompose/paperless/redisdata:/data:rw

  db:
    image: postgres
    container_name: PaperlessNGX-DB
    restart: on-failure:5
    volumes:
      - /home/ubuntu/docker/dockercompose/paperless/pgdata:/var/lib/postgresql/data:rw
    environment:
      POSTGRES_DB: paperless
      POSTGRES_USER: paperless
      POSTGRES_PASSWORD: paperless

  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx
    container_name: PaperlessNGX
    restart: on-failure:5
    depends_on:
      - db
      - redis
      - gotenberg
      - tika
    ports:
      - 8010:8000
    volumes:
      - /home/ubuntu/docker/dockercompose/paperless/data:/usr/src/paperless/data
      - /home/ubuntu/docker/dockercompose/paperless/media:/usr/src/paperless/media
      - /home/ubuntu/docker/dockercompose/paperless/export:/usr/src/paperless/export
      - /home/ubuntu/docker/dockercompose/paperless/consume:/usr/src/paperless/consume
    environment:
      PAPERLESS_REDIS: redis://redis:6379
      PAPERLESS_DBHOST: db
      USERMAP_UID: 
      USERMAP_GID: 
      PAPERLESS_TIME_ZONE: Europe/Vienna
      PAPERLESS_ADMIN_USER: 
      PAPERLESS_ADMIN_PASSWORD: 
      PAPERLESS_URL: 
      PAPERLESS_CSRF_TRUSTED_ORIGINS: 
      PAPERLESS_OCR_LANGUAGE: deu+eng
      PAPERLESS_TIKA_ENABLED: 1
      PAPERLESS_TIKA_GOTENBERG_ENDPOINT: http://gotenberg:3000/forms/libreoffice/convert#
      PAPERLESS_TIKA_ENDPOINT: http://tika:9998
      PAPERLESS_FILENAME_FORMAT_REMOVE_NONE: true
      PAPERLESS_FILENAME_FORMAT: "{created_year}/{correspondent}/{title}"

  gotenberg:
    image: gotenberg/gotenberg
    restart: on-failure:5
    container_name: PaperlessNGX-GOTENBERG
    ports:
      - 3000:3000
    command:
      - "gotenberg"
      - "--chromium-disable-routes=true"

  tika:
    image: ghcr.io/paperless-ngx/tika
    container_name: PaperlessNGX-TIKA
    ports:
      - 9998:9998
    restart: always

```

