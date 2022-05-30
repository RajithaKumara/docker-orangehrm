# OrangeHRM Open Source Docker Images

## Supported tags and respective Dockerfile links

- [`5.0-apache-bullseye`, `latest`](https://github.com/RajithaKumara/docker-orangehrm/blob/main/bullseye/apache/Dockerfile)
- [`5.0-fpm-bullseye`](https://github.com/RajithaKumara/docker-orangehrm/blob/main/bullseye/fpm/Dockerfile)
- [`5.0-fpm-alpine3.16`](https://github.com/RajithaKumara/docker-orangehrm/blob/main/alpine3.16/fpm/Dockerfile)

## How to use this image
#### Without docker-compose
```bash
$ docker run -d -p 80:80 --name orangehrm rajithakumara/orangehrm:5.0-apache-bullseye
```
#### With docker-compose
```yaml
version: "2"
services:
  server:
    image: rajithakumara/orangehrm:5.0-apache-bullseye
    ports:
      - "${APACHE_PORT}:80"
    networks:
       - orangehrm
    restart: always

  db:
    image: mariadb:10.2
    ports:
      - "${DB_PORT}:3306"
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
    volumes:
      - db-data:/var/lib/mariadb/102
    depends_on:
      - server
    networks:
      - orangehrm
    restart: always

volumes:
    db-data:

networks:
  orangehrm:
```
