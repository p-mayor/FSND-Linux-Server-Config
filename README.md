# FSND-Linux-Server-Config

Summary: An amazon lightsail instance was created and configured to serve a basic web application.

## 1. Responding to HTTP requests

Install apache2 to respond to HTTP requests:

```sudo apt-get install apache2```


## 2. Create the initial directory FlaskApp

Move to the /var/www directory and create the FlaskApp directory:
```sudo mkdir FlaskApp```

Note: FlaskApp can be named whatever you like.

Create another directory FlaskApp inside the initial directory. Then, move inside this directory and create two subdirectories named static and templates.

Directory structure so far:

```
|----FlaskApp
|---------FlaskApp
|--------------static
|--------------templates
```

Create the __init__.py file that will contain the flask application logic inside FlaskApp/FlaskApp. Add the code for your  flask app to the file. Save and close. Example code for initial testing: 
```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, I love Digital Ocean!"
if __name__ == "__main__":
    app.run()
```
## 3. Install Flask

Install pip and virtualenv:
```sudo apt-get install python-pip```
```sudo pip install virtualenv ```

Create a temporary environment: 
```sudo virtualenv venv```

Note: venv can be named whatever you like.

Now install flask in that environment. Activate the environment with:
```source venv/bin/activate```

Install flask inside the environment:
```sudo pip install Flask```

Test to see if the application is working with:
```sudo python __init__.py```

It should display “Running on http://localhost:5000/” or "Running on http://127.0.0.1:5000/". If you see this message, you have successfully configured the app.

Deactivate the virtual environment with ```deactivate```.

## 4. Configure and Enable a New Virtual Host

Create an apache configuration file for your app:
```sudo nano /etc/apache2/sites-available/FlaskApp.conf```

Add the following lines of code to the file to configure the virtual host. Be sure to change the ServerName to your domain or cloud server's IP address:

```
<VirtualHost *:80>
		ServerName mywebsite.com
		ServerAdmin admin@mywebsite.com
		WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
		<Directory /var/www/FlaskApp/FlaskApp/>
			Order allow,deny
			Allow from all
		</Directory>
		Alias /static /var/www/FlaskApp/FlaskApp/static
		<Directory /var/www/FlaskApp/FlaskApp/static/>
			Order allow,deny
			Allow from all
		</Directory>
		ErrorLog ${APACHE_LOG_DIR}/error.log
		LogLevel warn
		CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Save and close the file.

Enable the virtual host with the following command:
```sudo a2ensite FlaskApp```

## 5. Create .wsgi file

Move to the /var/www/FlaskApp directory and create a file named flaskapp.wsgi with following commands:
```
cd /var/www/FlaskApp
sudo nano flaskapp.wsgi
```

Add the following lines of code to the flaskapp.wsgi file:
```
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'Add your secret key'
```

Now your directory structure should look like this:
```
|--------FlaskApp
|----------------FlaskApp
|-----------------------static
|-----------------------templates
|-----------------------venv
|-----------------------__init__.py
|----------------flaskapp.wsgi
```

Now restart apache:
```sudo service apache2 restart```

## Additional info
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
