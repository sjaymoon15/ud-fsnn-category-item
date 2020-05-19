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

### Created virtualenv

    $ sudo virtualenv venv
    $ source venv/bin/activate

### Changed DB from sqlite to postgre and updated an argument for create_engine.

    - DB name : categoryitem
    - User: categoryitemuser

### Created a new flask-prod.conf file (/etc/apache2/sites-available/flask-prod.conf) and enable it with (sudo a2ensite flask-prod.conf).

flask-prod.conf content below;

```
<VirtualHost *:80>
    ServerName http://34.232.244.45.xip.io
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

## A list of any third-party resources you made use of to complete this project.

```
(manually installed packages)

sudo pip install flask packaging oauth2client redis passlib flask-httpauth
sudo pip install sqlalchemy flask-sqlalchemy psycopg2-binary bleach requests
```

## How to ssh as grader

```
ssh grader@34.232.244.45 -p 2200 -i <ssh key file path>
```
