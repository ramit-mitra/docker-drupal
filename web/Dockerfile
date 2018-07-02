FROM php:7.2-apache
USER root

RUN apt-get update && apt-get install -y && \
    apt-get install apt-utils zlib1g-dev git -y && \
    docker-php-ext-install zip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"

# RUN rm -rf /var/www/html && \
#     mkdir /var/www/html && \
#     git clone https://github.com/gobinathm/drupal-quickstart.git /var/www/html/

WORKDIR /var/www/html/

RUN git init && \
    git remote add origin https://github.com/gobinathm/drupal-quickstart.git && \
    git fetch && \
    git checkout 8.x && \
    git pull

RUN ./composer.phar install -o

EXPOSE [ 80, 443 ]