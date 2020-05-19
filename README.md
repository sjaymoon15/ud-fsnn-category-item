# Full Stack Web Developer Nanodegree ProjectL Linux Server Configuration

## The IP address and SSH port so your server can be accessed by the reviewer.

```
IP address (static): 34.232.244.45
SSH port: 2200
```

## The complete URL to your hosted web application.

```
http://34.232.244.45.xip.io
```

## A summary of software you installed and configuration changes made.

1. Created virtualenv

   $ sudo virtualenv venv
    $ source venv/bin/activate

2. Changed DB from sqlite to postgre and updated an argument for create_engine.

   - DB name : categoryitem
   - User: categoryitemuser

3. Created a new flask-prod.conf file (/etc/apache2/sites-available/flask-prod.conf) and enable it with (sudo a2ensite flask-prod.conf).

   flask-prod.conf content below;

   ```
   <VirtualHost *:80>
       ServerName 34.232.244.45
       ServerAlias 34.232.244.45.xip.io
       ServerAdmin jaymoon@34.232.244.45.xip.io
       WSGIScriptAlias / /var/www/flask-prod/flask-app/vagrant/catalog/flask-prod.wsgi
       WSGIDaemonProcess views python-path=/var/www/flask-prod/flask-app/vagrant/catalog:/var/www/flask-prod/env/lib/pyt$
       <Directory /var/www/flask-prod/flask-app/vagrant/catalog>
       WSGIProcessGroup views
       WSGIApplicationGroup %{GLOBAL}
           Order deny,allow
           Allow from all
       </Directory>
       Alias /static /var/www/flask-prod/flask-app/vagrant/catalog/static
       <Directory /var/www/flask-prod/flask-app/vagrant/catalog/static/>
           Order allow,deny
           Allow from all
       </Directory>
   </VirtualHost>
   ```

4. Configured the UFW

   Only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)

   ```
   $ sudo ufw allow 2200/tcp
   $ sudo ufw allow 80/tcp
   $ sudo ufw allow 123/udp
   $ sudo ufw enable
   ```

5. Installed and configured Apache to serve a Python mod_wsgi application
   ```
   $ sudo apt-get install apache2
   $ sudo apt-get install python-setuptools libapache2-mod-wsgi
   $ sudo service apache2 restart
   ```

## A list of any third-party resources you made use of to complete this project.

```
sudo pip install flask packaging oauth2client redis passlib flask-httpauth
sudo pip install sqlalchemy flask-sqlalchemy psycopg2-binary bleach requests
```

## How to ssh as grader

```
ssh grader@34.232.244.45 -p 2200 -i <ssh key file path>
```
