FROM ubuntu:17.10

RUN apt-get update \ 
    && apt-get install -y nginx curl nano vim sudo git supervisor \
    && apt-get install -y php7.1-mysql php7.1-mbstring php7.1-mcrypt php7.1-cli php7.1-curl php7.1-xml php7.1-tidy php7.1-fpm php7.1-intl php7.1-bcmath \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php --install-dir=/usr/bin --filename=composer

COPY default.conf /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
COPY www.conf /etc/php/7.1/fpm/pool.d/www.conf

EXPOSE 80

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN service php7.1-fpm start

CMD "/usr/bin/supervisord"