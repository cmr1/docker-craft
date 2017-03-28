# Docker Craft
Dockerized version of craft

Maintainer: Caleb Collins <kbcaleb@gmail.com>

Nginx
PHP:7-FPM
MySQL:5.6
Node

## Install
Pretty basic right now

### Checkout
```shell
git clone https://github.com/cmr1/docker-craft.git
```

### SSL Certs
You will need to put your SSL certificates in the app/conf directory and update the docker-compose.yaml file to point to them.
```conf
    volumes:
      - ./app/conf/nginx-partials:/etc/nginx/nginx-partials
      - ./app/conf/SOMEDOMAIN.com.crt:/etc/nginx/ssl/live/SOMEDOMAIN.com/SOMEDOMAIN.com.crt
      - ./app/conf/SOMEDOMAIN.com.key:/etc/nginx/ssl/live/SOMEDOMAIN.com/SOMEDOMAIN.com.key
      - ./app/conf/default.conf:/etc/nginx/conf.d/default.conf
```
### Deploy
```shell
cd docker-craft
docker-compose up
```
The first time it runs it will take a while to import the SQL dump because of the limited size and IO of the MySQL container.
You can connect to the site once you see the following.
```shell
mysql_1      | Version: '5.6.35'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
```
After MySQL has loaded the data the first time all subsequent loads will shows this as the final prompt
```shell
compose      | npm info ok
compose      | Running "uglify:dev" (uglify) task
compose      | >> 1 file created.
compose      |
compose      | Running "sass:dev" (sass) task
compose      |
compose      | Running "autoprefixer:dist" (autoprefixer) task
compose      | >> 1 autoprefixed stylesheet created.
compose      |
compose      | Done, without errors.
compose exited with code 0
```
You can always background the whole thing with
```shell
docker-compose up -d
```

## Debug

## Future Additions
* Will use RDS in prod
* Utilize EFS for new containers
* tasks assigned to nginx boxes
