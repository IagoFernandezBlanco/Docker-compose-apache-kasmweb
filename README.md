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

 
