# Nginx image for Symfony2 projects.
FROM ubuntu:14.04.2

MAINTAINER Filipp K. <filippk8@gmail.com>

ENV NGINX_VERSION 1.8.0-1+trusty1

# Nginx repository.
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:nginx/stable

# Install nginx.
RUN apt-get update
RUN apt-get install -y nginx=${NGINX_VERSION}

# Cleanup FS.
RUN rm -rf /var/lib/apt/lists/*
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

# Configure SSL.
COPY ./default.crt /etc/ssl/certs/default.crt
COPY ./default.key /etc/ssl/private/default.key

# Configure WWW pool.
COPY ./default /etc/nginx/sites-available/default

# Forward request and error logs to docker log collector.
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Define mountable directories.
VOLUME /var/www

# Define default command.
CMD ["nginx"]

# Expose HTTP port.
EXPOSE 80

# Expose HTTPS port.
EXPOSE 443
