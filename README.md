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

### Httpd.conf 
<code>
  Include conf/extra/httpd-vhosts.conf 
 </code>
 ### httpd-vhosts.conf
 <code>
  <VirtualHost *:80>
    
    DocumentRoot "/usr/local/apache2/htdocs/index1.html"
    ServerName paxina1.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>

<VirtualHost *:80>
    
    DocumentRoot "/usr/local/apache2/htdocs/index2.html"
    ServerName paxina2.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>
</code>

### DNS
<code>
  ;
; BIND data file for example.com
;
$TTL	604800
@	IN	SOA	example.com root.example.com. (
			      2		; Serial
			 604800		; Refresh
			  86400		; Retry
			2419200		; Expire
			 604800 )	; Negative Cache TTL
;
@	IN	NS	ns.example.com.
@	IN	A	10.0.0.10
@	IN	AAAA	::1
ns  IN  A   10.0.0.254
example.com. IN  A   10.0.0.10
paxina1 IN  CNAME   example.com.
paxina2 IN  CNAME   example.com.
</code>

### Zone
<code>
  zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};
</code>

### Forwarders
<code>
forwarders {
	8.8.8.8; //google.com
	8.8.4.4; //google.com
	};
 </code>
 
 ### VirtualHosts
 <code>
  <VirtualHost *:80>
    
    DocumentRoot "/usr/local/apache2/htdocs/index3.html"
    ServerName paxina3.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>

<VirtualHost *:80>
    
    DocumentRoot "/usr/local/apache2/htdocs/index4.html"
    ServerName paxina4.example.com
    ErrorLog "logs/dummy-host2.example.com-error_log"
    CustomLog "logs/dummy-host2.example.com-access_log" common
</VirtualHost>
  </code>
  
### Certified
<code>
  apt get install openssl-server

openssl genrsa -out key.key 2048

openssl req -new -key key.key -out certificado.csr
  
  openssl x509 -req -days 365 -in certificado.csr -signkey key.key -out certificado.crt
</code>

### SSl
<code>
  <VirtualHost *:443>
    </code>
<code>
  nano /etc/apache2/ports.conf
  </code>

### HSTS
  <code>
    a2enmod headers

service apache2 restart

nano /etc/apache2/sites-availables/paxina3.conf

<VirtualHost *:443>
//añadimos lo siguiente dentro del VirtualHost

Headers always set Strict=Trasport-Security "max-age=999999999; includessubdomain"
</VirtualHost>
  </code>

  
