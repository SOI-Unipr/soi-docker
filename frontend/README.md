## build the apache image
```
docker build -t apache2:latest .
```
## run the image - app can be reached out using http://localhost:8080/
```
docker run -dit --name todo-app -p 8080:80 apache2
```
## get the ip of the server using check the connectivity
```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' todo-server
```
## customize apache configuration file with virtual hosting
```
docker run --rm httpd:2.4 cat /usr/local/apache2/conf/httpd.conf > my-httpd.conf
```
```
<VirtualHost *:80>
    ServerName soi-labdocker.unipr.it
    ServerAlias www.soi-labdocker.unipr.it soi-labdocker.unipr.it
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www
    LogLevel info
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    ProxyPass     /api/        http://10.88.0.11:8000/
</VirtualHost>
```
enable proxy modules

```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
```
## add this line to DOCKER file
```
COPY ./my-httpd.conf /usr/local/apache2/conf/httpd.conf
```
## add this line to /etc/hosts file (using sudo)
```
127.0.0.1       soi-labdocker.unipr.it www.soi-labdocker.unipr.it
```
## run the image using network
```
docker run -dit --name todo-app -p 8080:80 --network todo-app-network apache2
```

## if you want to install telnet or wget
```
apt-get update
apt-get install telnet
apt-get install wget
```
