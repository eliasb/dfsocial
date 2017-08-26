#docker build .
FROM eliasny/drupal-open-social:8.3.7-apache

MAINTAINER Elias Barbosa <info@eb8.com>

WORKDIR /var/www/html

# Add a cron job to backup the website.
RUN mkdir /html
RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /var/www/html/ /html/' >> /etc/crontab
# RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /html/ /var/www/html/' >> /etc/crontab