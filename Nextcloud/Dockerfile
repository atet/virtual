FROM balenalib/raspberry-pi-debian:buster
MAINTAINER Athit Kao (github.com/atet)
RUN printf "deb-src http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi" >> \
   /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y apt-utils git
RUN apt-get install -y apache2 python-mysqldb php php-gd php-curl php-zip php-xml php-mbstring \
   libapache2-mod-php php-mysql
WORKDIR "/var/www/html"
RUN git clone https://github.com/atet/nextcloud.git
RUN mkdir -p /var/www/html/nextcloud/data
RUN chown www-data:www-data /var/www/html/nextcloud/data
RUN chmod 750 /var/www/html/nextcloud/data
RUN chown www-data:www-data /var/www/html/nextcloud/config /var/www/html/nextcloud/apps
EXPOSE 80
CMD ["apachectl", "-D", "FOREGROUND"]