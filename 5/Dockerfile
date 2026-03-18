FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean

EXPOSE 80

COPY index.html /var/www/html/index.html

CMD ["apachectl", "-D", "FOREGROUND"]