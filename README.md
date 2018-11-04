# Project Three: Linux Server Configuration
This project is part of the FSND course from Udacity. In this project I set up linux server for the grader to access and preview my final project.

## General
IP: 13.126.93.116

## Steps:

1- Get the Server:
Reference: [1](https://medium.com/@mariasurmenok/creating-a-server-with-amazon-lightsail-11c377cf814c)

2- SSH in reviewer notes.

3- Update all installed packages:

```
sudo apt-get update
sudo apt-get upgrade
```


4- Change SSH port to 2200:
using this command, and going to the line where it says Port 20, change to 2200

```
sudo nano /etc/ssh/sshd_config
```

Reference: [1](https://serversforhackers.com/c/configuring-sshd-on-the-server)

5- Configure Firewall
Using the security lessons videos and the reference below.

```
sudo ufw allow www
sudo ufw allow 123/udp
sudo ufw allow 2200
```

Reference: [1](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

6- Create grader user
```
sudo adduser grader
```

7- Give grader Sudo
```
sudo usermod -aG sudo grader
```
Reference: [1](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart)

8- Create an SSH
Create ssh key in local machine using 
```
ssh-keygen
```
go back to server, switch to grader user using
```
su -u grader
```
add .ssh and .ssh/authorized_keys file
```
mkdir /.ssh/
nano /.ssh/authorized_keys   # copy the key here
```
You can now connect using the command:
```
$ ssh -i /c/users/user/.ssh/grader grader@13.126.93.116 -p 2200
```

9- Configure the local timezone to UTC.
```
sudo dpkg-reconfigure tzdata
```

Reference: [1](https://askubuntu.com/questions/323131/setting-timezone-from-terminal)

10- Install apache
```
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi-py3
```


11- Install postgreSQL
```
sudo apt install postgresql
```
Create the database and give permission:
```
CREATE USER grader WITH PASSWORD 'grader';
CREATE DATABASE catalog WITH OWNER catalog;
```
Reference: [1](https://stackoverflow.com/a/34448413/2022948)


12- Install Git
```
sudo apt-get install git
```

13- Clone the project
```
sudo git clone https://github.com/alioh/Udacity-FSND-P2.git catalog
```

install all libraries and requirements:
```
pip install flask
pip install Flask-SQLAlchemy
pip install flask-oidc
pip install okta
pip install sqlalchemy
pip install flask_wtf
pip install wtforms
pip install flask_bootstrap
```

14- WSGI Application
edit the file
```
sudo nano /etc/apache2/sites-available/000-default.conf
```
Reference: [1](http://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/), [2](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts)

Restart to launch
```
sudo service apache2 restart
```

[Virtual environment reference](https://vishnut.me/blog/ec2-flask-apache-setup.html)