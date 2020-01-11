FROM arm32v6/alpine
RUN apk update
RUN apk add --update --no-cache lighttpd php-cgi
RUN apk add --update --no-cache nextcloud-mysql
RUN mv /etc/lighttpd/lighttpd.conf /etc/lighttpd/lighttpd.conf.BAK
RUN sed "s/#   include \"mod_fastcgi.conf\"/   include \"mod_fastcgi.conf\"/" \
   /etc/lighttpd/lighttpd.conf.BAK > /etc/lighttpd/lighttpd.conf
RUN ln -s /usr/share/webapps/nextcloud /var/www/localhost/htdocs
RUN mkdir -p /var/www/localhost/htdocs/nextcloud/data
RUN chmod 750 /var/www/localhost/htdocs/nextcloud/data
RUN adduser -u 82 -D -S -G www-data www-data
RUN chown www-data:www-data /var/www/localhost/htdocs/nextcloud/data
RUN chown www-data:www-data /var/www/localhost/htdocs/nextcloud/config
RUN chown www-data:www-data /var/www/localhost/htdocs/nextcloud/apps
RUN cp /var/www/localhost/htdocs/nextcloud/index.html /var/www/localhost/htdocs/index.html 
RUN printf "$(date)<br><?php phpinfo(); ?>" > /var/www/localhost/htdocs/index.php
RUN mkdir /var/run/lighttpd
RUN touch /var/run/lighttpd/php-fastcgi.socket
RUN chown -R lighttpd:lighttpd /var/run/lighttpd
EXPOSE 80
CMD ["/usr/sbin/lighttpd", "-f", "/etc/lighttpd/lighttpd.conf"]