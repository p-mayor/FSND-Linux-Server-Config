# FSND-Linux-Server-Config

Summary: An amazon lightsail instance was created and configured to serve a basic web application.

## 1. Responding to HTTP requests

Install apache2 to respond to HTTP requests:

```sudo apt-get install apache2```

IP: 52.14.72.239 SSH Port: 2200

Complete URL: http://ec2-52-14-72-239.us-east-2.compute.amazonaws.com/

Packages installed: apache2, libapache2-mod-wsgi, flask, postgresql, pip, virtualenv, sqlalchemy, fail2ban

UFW configuration:
```
To                         Action      From
--                         ------      ----
22                         DENY       Anywhere                  
2200/tcp                   ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
22 (v6)                    DENY      Anywhere (v6)             
2200/tcp (v6)              ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6) 
```

Third Party Resources:

https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04
