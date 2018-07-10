# Linux Server Configuration Project

Udacity Front End Developer - Clay Haberly 7/9/2018
Written with Python 2.7.13

## Purpose

The purpose of the project is to learn how to setup, access, secure and configure a bare bones Linux Apache server to host a web application previously created.

## Details for the reviewer

IP Address: 18.217.251.235

SSH Port: 2200

URL: 18.217.251.235

## Summary of software installion and configuration changes

### Server Updates

The following commands were issued to update the software on the Amazon LightSail Linux machine:

```
sudo apt-get update
sudo apt-get upgrade
```

Created new user: grader

Added the user grader to the sudoers file with appropiate permission

Configured SSH to use a non-default port via the sshd_config file by disabling port 22 and opening port 2200

Also in the sshd_config we disabled root login

Created SSH key pairs with the ssh-keygen utility

Stored the public key in .ssh/authorized_keys

Utilized ufw to configure firewall rules as follows:
default deny incoming
default allow outgoing
allow 2200/tcp
allow 80/tcp
allow 123/udp

Changed the timezone on the server using:
```
sudo dpkg-reconfigure tzdata
```
inPostGreSql, cttreated user ctatalog and gave it CREATEDB permissions
revoked permission for public and granted all for catalog


In the following python programs:
catalog_app.py
create_db.py
populate_db.py

The following line was changed from:

`engine = create_engine('sqlite:///catalog.db')`

To:

`engine = create_engine('postgresql://catalog:catalog@localhost/catalog')`


Verified remote access was disable for postgresql via the `/etc/postgresql/9.1/main/pg_hba.conf' file


Also in the catalog_app.py program the follwing lines were changed from:

`oauth_flow = flow_from_clientsecrets('client_secrets.json', scope='')`
`CLIENT_ID = json.loads(open('client_secrets.json', 'r').read())['web']['client_id']`
to:

`oauth_flow = flow_from_clientsecrets('/var/www/html/CatalogProject/client_secrets.json', scope='')`
`CLIENT_ID = json.loads(open('/var/www/html/CatalogProject/client_secrets.json', 'r').read())['web']['client_id']`

This correction was needed to point the client_secrets.json to the correct location on the server.

Created an `.htaccess` file in `/var/www/html` so the `.git` directory would not be accesible by the public

After submission, the server could not be reached. I had to enable port 2200 on my LightSail management console under networking.

## Installed the following software

apache2
libapache2-mod-wsgi
Git
python-flask
python-Sqlalchemy
python-psycopg2
PostGresSql
Oauth2client
httplib2

## Resources used

https://hk.saowen.com/a/0a0048ca7141440d0553425e8df46b16cdf4c13f50df4c5888256393d34bb1b9

https://medium.com/@hvedam/aws-light-sail-and-flask-25f093081ea

https://github.com/harushimo/linux-server-configuration/blob/master/README.md

http://Google.com

https://www.jakowicz.com/flask-apache-wsgi/

https://www.pythoncentral.io/how-to-install-sqlalchemy/

https://stackoverflow.com/questions/12906351/importerror-no-module-named-psycopg2

http://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html

https://stackoverflow.com/questions/6142437/make-git-directory-web-inaccessible

### License

MIT
