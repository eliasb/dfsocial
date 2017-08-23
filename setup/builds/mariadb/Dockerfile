#docker build .
FROM mariadb

MAINTAINER Elias Barbosa <info@eb8.com>

RUN mkdir -p /root/mysql

RUN apt-get -y update
RUN apt-get -y --fix-missing install cron
RUN apt-get -y --fix-missing install rsync
RUN apt-get -y --fix-missing install nano

RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /var/lib/mysql/ /root/mysql/' >> /etc/crontab
RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /root/mysql/ /var/lib/mysql/' >> /etc/crontab