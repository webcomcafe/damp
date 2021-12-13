FROM httpd:2.4

RUN apt-get update \
    && apt-get install -y iputils-ping vim

COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf

COPY ./httpd-ssl.conf /usr/local/apache2/conf/extra/httpd-ssl.conf