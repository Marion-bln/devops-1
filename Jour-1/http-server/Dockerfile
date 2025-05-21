FROM httpd:alpine

# Active les modules nécessaires au reverse proxy
RUN echo "LoadModule proxy_module modules/mod_proxy.so\n\
LoadModule proxy_http_module modules/mod_proxy_http.so\n\
\n\
<VirtualHost *:80>\n\
    ProxyPreserveHost On\n\
    ProxyPass / http://backend-api:8080/\n\
    ProxyPassReverse / http://backend-api:8080/\n\
</VirtualHost>" > /usr/local/apache2/conf/httpd.conf
