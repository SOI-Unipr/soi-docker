## build the apache image
docker build -t apache2 .

## run the image - app can be reached out using http://localhost:8080/
docker run -dit --name todo-app -p 8080:80 apache2

## customize apache configuration file
docker run --rm httpd:2.4 cat /usr/local/apache2/conf/httpd.conf > my-httpd.conf

```
<VirtualHost *:80>
    ServerName soi-labdocker
    ServerAlias www.soi-labdocker soi-labdocker
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www
    LogLevel info
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    ProxyPass     /api/        http://172.17.0.99:8000/
</VirtualHost>
```
## add this line to DOCKER file
COPY ./my-httpd.conf /usr/local/apache2/conf/httpd.conf

## add this line to /etc/hosts file (using sudo)
127.0.0.1       soi-labdocker www.soi-labdocker

## run the image usgin network
docker run -dit --name todo-app -p 8080:80 --network todo-app-network apache2
