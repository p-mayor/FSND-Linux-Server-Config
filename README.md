# FSND-Linux-Server-Config

IP: 52.14.72.239 SSH Port: 2200

Complete URL: http://ec2-52-14-72-239.us-east-2.compute.amazonaws.com/

Packages installed: apache2, libapache2-mod-wsgi, flask, postgresql, pip, virtualenv

UFW configuration:
```
To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere                  
2200/tcp                   ALLOW       Anywhere                  
80/tcp                     ALLOW       Anywhere                  
22 (v6)                    ALLOW       Anywhere (v6)             
2200/tcp (v6)              ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6) 
```

Third Party Resources:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
