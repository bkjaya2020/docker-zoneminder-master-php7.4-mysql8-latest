# docker-zoneminder-master-php7.4-mysql8-latest
Zoneminder-master-latest ,docker images with php 7.4 ,Mysql 8 &amp; MSMTP

This image has been created on ubuntu:eoan with zoneminder-master/ubuntu eoan main
To pull the Repository from the dockerhub
please refer the following link

https://hub.docker.com/r/bkjaya1952/docker-zoneminder-master-mysql8


Usage :

To create a Zonminder-master docker container (name zm)with php 7.4 ,mysql 8 & msmtp

On the Ubuntu terminal enter the following commands

<code>sudo docker create -t -p 8080:80 --shm-size=4096m --name zm --privileged=true bkjaya1952/docker-zoneminder-master-php7.4-mysql8:latest</code>

<code>sudo docker start zm</code>

(You will have to configure the running zm container for mysql 8 ,zm data base and make some changes to start apache and zoneminder during the first run .)

<code>sudo docker exec -t -i zm /bin/bash</code>

(Now  you will be with in the zm container.

Make changes as follows)

<code>mysql -uroot -p < /usr/share/zoneminder/db/zm_create.sql</code>

<code>mysql</code>

<code>CREATE USER 'zmuser'@localhost IDENTIFIED WITH mysql_native_password BY 'zmpass';</code>

<code>GRANT ALL PRIVILEGES ON zm.* TO 'zmuser'@'localhost' WITH GRANT OPTION;</code>

<code>FLUSH PRIVILEGES ;</code>

<code>quit</code>

m<code>ysqladmin -uroot -p reload</code>

<code>exit</code>

<code>sudo docker restart zm</code>
 
 <code>sudo docker exec -t -i zm /bin/bash</code>

<code>http://localhost:8080/zm/</code>

Note:- If you find any timezone mismatch in zoneminder logs , correct it as follows.( ie for America/New_York )

On the ubuntu terminal

<code>sudo docker exec -t -i zm /bin/bash

<code>dpkg-reconfigure tzdata</code>

Then edit your timezone

<code>exit</code>


