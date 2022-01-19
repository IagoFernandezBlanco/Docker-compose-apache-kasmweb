# Docker-compose-apache-kasmweb

## Creación de tres contenedores docker

```
docker-compose up
  version: "3.3"  
services:  
 apaches-server:  
   image: httpd:latest  
   networks:  
      br02:  
        ipv4_address: 10.1.0.10  
   ports:  
     - 80:80  
   volumes:  
     - apache-servidor:/usr/local/apache2/conf  
     - apache-servidor2:/usr/local/apache2/htdocs  
 kasmweb-cliente:  
   image: kasmweb/desktop:1.10.0-rolling  
   networks:  
      br02:  
        ipv4_address: 10.1.0.20  
   ports:  
    - 6901:6901  
   environment:  
    - VNC_PW=password   
   stdin_open: true  # docker run -i  
   tty: true         # docker run -t  
   dns:   
    - 10.1.0.254  
volumes:  
 apache-servidor:  
   external: true  
 apache-servidor2:  
   external: true     
networks:  
  br02:     
    external: true  
```
## Recursos de interes
[Docker](https://www.docker.com/)  
[Docker Hub-Apache](https://hub.docker.com/_/httpd)  
[Docker Hub-Kasmweb](https://hub.docker.com/r/kasmweb/desktop/tags)
## Comandos
<code>
docker pull kasmweb/chrome:1.10.0-rolling
</code>
<code>
docker pull httpd:latest
</code>

![Docker](https://r.search.yahoo.com/_ylt=AwrJ6tU1Luhh_XIAqVGV.Qt.;_ylu=c2VjA3NyBHNsawNpbWcEb2lkAzUwYWZlMzBmZDg2NmUyZTVkYzZiNzNhNWUyNjJkMmM0BGdwb3MDMwRpdANiaW5n/RV=2/RE=1642634933/RO=11/RU=http%3a%2f%2fblog.xebia.fr%2f2016%2f04%2f08%2fdocker-pattern-conteneur-de-build%2f/RK=2/RS=urBF2JG_bUcw7TLwxwWvwO9DOeY-)
