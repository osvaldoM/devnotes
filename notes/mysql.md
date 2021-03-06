[disable safe_mode](https://serverpilot.io/community/articles/how-to-disable-strict-mode-in-mysql-5-7.html)


### Running different mysql version on the same host using docker container


To install Docker on your machine, execute following command on your shell.

`curl -sSL https://get.docker.com/ | sh`


Execute following command; this will download MySQL 5.5 image and will spin off the container. This container will have MySQL 5.5 installed on port 3306. But on the host machine, port 3310 will be forwarded.

`sudo docker run --name mysql-55-container -p 127.0.0.1:3310:3306 -e MYSQL_ROOT_PASSWORD=rootpassword -d mysql:5.5`

Connect to MySQL 5.5

`mysql -u root -p --host=127.0.0.1 --port=3310`



Source: [https://www.codementor.io/@arpitbhayani/setup-multiple-mysql-servers-with-different-versions-docker-du107solq](https://www.codementor.io/@arpitbhayani/setup-multiple-mysql-servers-with-different-versions-docker-du107solq)


### Full Text Search tutorial

https://www.mysqltutorial.org/mysql-ngram-full-text-parser/
