# docker-nginx-php7-mysql-phpmyadmin

version: '2'

services:
  nginx:
    image: bencomtech/nginx:1.12
    ports:
      - 80:8080
      - 443:8443
    depends_on:
      - phpfpm
    volumes:
      - ./dockers/logs:/opt/bitnami/nginx/logs
      - ./dockers/nginx:/bitnami/nginx
      - ./web:/app

  phpfpm:
    image: lyberteam/php-fpm7.0
    volumes:
      - ./dockers/phpfpm:/bitnami/php-fpm
      - ./web:/app

  mariadb:
    image: bencomtech/mariadb:10.2
    environment:
      - MARIADB_ROOT_PASSWORD=p@ssword
    volumes:
      - ./dockers/mariadb:/bitnami/mariadb

  phpmyadmin:
    image: bencomtech/phpmyadmin:4.7
    ports:
      - 8000:80
    depends_on:
      - mariadb
