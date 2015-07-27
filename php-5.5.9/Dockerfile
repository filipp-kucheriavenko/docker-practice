# PHP FPM image
FROM ubuntu:14.04.2

MAINTAINER Filipp K. <filippk8@gmail.com>

ENV PHP_VERSION 5.5.9+dfsg-1ubuntu4.11
ENV PHP_XDEBUG_VERSION 2.2.3-2build1

# Update source list.
RUN apt-get update

# Install FPM and CLI.
RUN apt-get install -y php5-fpm=${PHP_VERSION}
RUN apt-get install -y php5-cli=${PHP_VERSION}

# Install extensions.
RUN apt-get install -y php5-curl=${PHP_VERSION}
RUN apt-get install -y php5-mysql=${PHP_VERSION}

# Install XDebug
RUN apt-get install -y php5-xdebug=${PHP_XDEBUG_VERSION}
COPY ./xdebug.ini /etc/php5/mods-available/xdebug.ini

# Cleanup APT.
RUN rm -rf /var/lib/apt/lists/*

# Configure FPM WWW pool
RUN sed -i 's/;daemonize = yes/daemonize = no/' /etc/php5/fpm/php-fpm.conf
COPY ./www.conf /etc/php5/fpm/pool.d/www.conf

# Forward error logs to docker log collector
RUN ln -sf /dev/stderr /var/log/fpm-php.www.log

# Define mountable directories.
VOLUME /var/www

# Expose FPM port.
EXPOSE 9000

# Copy entry-point script
COPY ./entry-point.sh /entry-point.sh
ENTRYPOINT ["/entry-point.sh"]

# Define default command.
CMD ["php5-fpm"]