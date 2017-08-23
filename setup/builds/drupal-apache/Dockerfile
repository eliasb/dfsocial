#docker build .
FROM drupal:8.2.3-apache

MAINTAINER Elias Barbosa <info@eb8.com>

RUN apt-get update && \
DEBIAN_FRONTEND="noninteractive" apt-get install -y \
git \
nano \
cron \
rsync \
wget \
curl \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php && \
mv composer.phar /usr/local/bin/composer

# Install Drush 8 (master) as phar.
RUN curl http://files.drush.org/drush.phar -L -o /usr/local/bin/drush && \
chmod +x /usr/local/bin/drush

# Install Drupal Console.
RUN composer require drupal/console:~1.0 \
             --prefer-dist \
             --optimize-autoloader \
             --sort-packages

# Add a cron job to backup the website.
RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /var/www/html/ /html/' >> /etc/crontab
RUN echo '* * * * * root /usr/bin/rsync -a --ignore-errors /html/ /var/www/html/' >> /etc/crontab