# Linux Server Setup

### Project Overview
This is project #5 of **Udacity's Full Stack Web Developer Nanodegree**.
The main task is to configure a baseline installation of Ubuntu Linux
on a virtual machine, and use it host a [Flask web application][1] 
developed earlier in the course. Udacity provided the Amazon AWS development
environment for this project.

### Hosted Web App

The deployed web application can be accessed at
http://ec2-54-148-92-221.us-west-2.compute.amazonaws.com/. 

The use of a web browser such as Google Chrome in "incognito" mode is recommended.

### Server Login

The server can be accessed as the new user 'grader'at the public IP address 54.148.92.221
and using SSH port 2200 with `ssh -i ~/.ssh/udacity grader@54.148.92.221 -p 2200`, where
`~/.ssh/udacity` is the location of the key.

### Step by Step Installation
This section outlines the different stages of installation in two parts:
**Server Setup and Deployment of Web App**, which presents how the project
meets the basic Udacity requirements, and **Additional Functionalities**, 
which describes the steps taken to exceed minimum specifications. Links to 
third-party resources used are also included in this section. 

#### Server Setup and Deployment of Web App

##### 1. Access the development environment
The Amazon AWS development environment is available to FSWD Nanodegree
students through their [Udacity account][2].

The public IP address of the virtual machine created and used in this project
is 54.148.92.221.

##### 2. SSH into server as root user
The steps to access the Ubuntu Linux server as the root user for the first
time are:

1. Note public IP address of virtual machine: 54.148.92.221.
2. Download private key provided by Udacity.
3. Move the private key file into the folder ~/.ssh:  
`$ mv ~/Downloads/udacity_key.rsa ~/.ssh/`
4. Set file rights (only owner can write and read.):  
`$ chmod 600 ~/.ssh/udacity_key.rsa`
5. SSH into the instance:  
`$ ssh -i ~/.ssh/udacity_key.rsa root@54.148.92.221` 

Source: [Udacity][3]

##### 3. Update all currently installed packages
The steps to update the packages installed on the server are:

1. Update the list of available packages and their versions:  
`$ sudo apt-get update`
2. Install newer vesions of packages you have:  
`$ sudo sudo apt-get upgrade`

Sources: [Ask Ubuntu][4]

##### 4.Configure the local timezone to UTC.
The steps to configure the timezone are:

1. Open timezone selection:    
`$ sudo dpkg-reconfigure tzdata`
2. Select:   
`Geographic area: None of the above`    
3. Select:   
`UTC`

Source: [Digital Ocean][5]

##### 5. Create new user 'grader' with sudo permission
The steps to create a new user 'grader' that has sudo permission are:

1. Create a new user:  
`$ adduser grader`
2. Open the sudo configuration file:  
`$ visudo`
3. Edit the configuration file adding the following line below `root ALL...`:  
`grader ALL=(ALL:ALL) ALL`
4. Check that 'grader' was added by listing all users:    
`$ cut -d: -f1 /etc/passwd`
5. Enable password login in ssh config file to allow grader to log in:   
In `$ sudo nano /etc/ssh/sshd_config` set `PasswordAuthentication` to `yes`.
6. To switch to grader user:
`$sudo su - grader`

Sources: [Ask Ubuntu][7], [Ask Ubuntu][8], [Digital Ocean][6]

##### 6. Enable key based authentication for grader

1. Generate a SSH key pair on the local machine:  
`$ ssh-keygen`
2. Confirm the file path and name for new key pair:  
For example `$ /Users/Udacity/.ssh/udacity`
3. Optionally, enter a passphrase for the new key pair
4. Log in as grader and create .ssh directory in home directory:  
`$ mkdir .ssh`
5. Create `authorized_keys` to store all public keys used by grader:   
`$ touch .ssh/authorized_keys`
6. On the local machine open udacity.pub and copy its contents:  
`$ sudo cat .ssh/udacity.pub`
7. Paste the copied key into grader's `authorized_keys` file:  
`$ sudo nano authorized_keys`
8. Set permissions on `.ssh` directory and `authorized_keys` file:   
 `$ chmod 700 .ssh`
 `$ chmod 644 .ssh/authorized_keys `

Source: [Udacity][9]

##### 7. Change the SSH port to 2200 and disable root user
The steps to change SSH port to 2200 and disable root user access are:

1. Open the SSH config file:   
 `$ sudo nano /etc/ssh/sshd_config`
2. Change port value from 22 to 2200    
 `Port 2200`
3. Disable root user access:    
`PermitRootLogin no`
4. Disable password authentication:    
`PasswordAuthentication no`
5. Add the following lines, exit and save:    
`UseDNS no`   
`AllowUsers grader`   
6. Restart SSH:    
`service ssh restart`    

Source: [Ask Ubuntu][10]

##### 8. Configure the Uncomplicated Firewall (UFW)
The steps to configure the Uncomplicated Firewall (UFW) to only allow incoming
connections for SSH (port 2200), HTTP (port 80), and NTP (port 123) are:

1. Turn on UFW:    
`$ sudo ufw enable`
2. Allow incoming TCP packets on port 2200 (SSH):   
`$ sudo ufw allow 2200/tcp`
3. Allow incoming TCP packets on port 80 (HTTP):    
`$ sudo ufw allow 80/tcp`
4. Allow incoming UDP packets on port 123 (NTP):    
`$ sudo ufw allow 123/udp`

Source: [Digital Ocean][11]

##### 9. Install and configure Apache to serve a Python mod_wsgi application
The steps to install and configure Apache to serve a Python mod_wsgi application are:

1. Install Apache:   
`$ sudo apt-get install apache2`
2. Open browser and visit public IP address to load "It works!" page
3. Install **mod_wsgi** tool and helper package **python-setuptools**:    
`$ sudo apt-get install python-setuptools libapache2-mod-wsgi`
4. Restart Apache server:   
`$ sudo service apache2 restart`

Source: [Udacity blog][12]

##### 10. Install Flask and deploy a sample application
This entails installing mod_wsgi (if not previously installed), creating
the Flask app, installing Flask, configuring and enabling a new virtual host,
creating the .wsgi file, and updating modules and packages. 

###### 1. Install and Enable mod_wsgi
1. Install mod_wsgi:     
`$ sudo apt-get install libapache2-mod-wsgi python-dev`
2. Enable mod_wsgi:    
`sudo a2enmod wsgi`

###### 2. Creating a Flask App
1. Move to the /var/www directory:   
`$ cd /var/www`
2. Create catalog directory and move inside it:    
`$ sudo mkdir catalog`
`$ cd catalog`
3. Within catalog, create another catalog directory and move inside it:   
`$ sudo mkdir catalog`
`$ cd catalog`
4. Create two subdirectories named static and templates:   
`$ sudo mkdir static templates`
5. The structure within `/var/www` should be the following:   
|----catalog   
|---------catalog   
|--------------static   
|--------------templates   
6. Create the `__init__.py` file that will contain the flask application:
`$ sudo nano __init__.py`
7. Open `__init__.py`, add the code from step 8, exit and save:   
`$ sudo nano __init__.py`  
8. Paste in the following code:  
```python
from flask import Flask  
app = Flask(__name__)  
@app.route("/")  
def hello():  
  return "Hello, Udacity!"  
if __name__ == "__main__":  
  app.run()  
```

###### 3. Install Flask
1. Install pip:    
`$ sudo apt-get install python-pip`
2. Install virtualenv through pip:    
`$ sudo pip install virtualenv`
3. Create virtual environment 'venv':    
`$ sudo virtualenv venv`
4. Activate virtual environment:    
`$ source venv/bin/activate`
5. Install Flask within virtual environment:    
`$ sudo pip install Flask`
6. Test if the app is running after running:
`$ sudo python __init__.py`
7. Deactivate the environment:   
`$ deactivate`

###### 4. Configure and Enable a New Virtual Host
1. Issue the following command to create catalog.conf:     
`$ sudo nano /etc/apache2/sites-available/catalog.conf`
2. Paste in the following lines of code (customize public IP and folders):        
```
  <VirtualHost *:80>
      ServerName 54.148.92.221
      ServerAdmin admin@54.148.92.221
      WSGIScriptAlias / /var/www/catalog/catalog.wsgi
      <Directory /var/www/catalog/catalog/>
          Order allow,deny
          Allow from all
      </Directory>
      Alias /static /var/www/catalog/catalog/static
      <Directory /var/www/catalog/catalog/static/>
          Order allow,deny
          Allow from all
      </Directory>
      ErrorLog ${APACHE_LOG_DIR}/error.log
      LogLevel warn
      CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>
```
3. Enable the virtual host:     
`$ sudo a2ensite catalog`

###### 4. Create the .wsgi file
1. Create a file named catalog.wsgi:   
`$ sudo nano /var/www/catalog.wsgi`
2. Add the following lines of code:    
```
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/catalog/")

from catalog import app as application
application.secret_key = 'Add your secret key'`
```
3. Restart Apache:    
`$ sudo service apache2 restart`

###### 5. Install modules and packages  
1. Activate virtual environment:   
`$ source venv/bin/activate`
2. Install httplib2 module in venv:   
`$ pip install httplib2`
3. Install requests module in venv:   
`$ pip install requests`
4. *Install flask.ext.seasurf (only seems to work when installed globally):   
`$ *sudo pip install flask-seasurf`
5. Install oauth2client.client:   
`$ sudo pip install --upgrade oauth2client`
6. Install SQLAlchemy:   
`$ sudo pip install sqlalchemy`
7. Install the Python PostgreSQL adapter psycopg:   
`$ sudo apt-get install python-psycopg2`
8. Deactivate the environment:   
`$ deactivate`

Sources: [Digital Ocean][13], [github.com/stueken][14]

##### 11. Install and configure PostgreSQL
The steps to install and configure PostgreSQL are:

1. Install PostgreSQL:   
`$ sudo apt-get install postgresql postgresql-contrib`
2. Ensure that no remote connections are allowed:    
`$ sudo nano /etc/postgresql/9.3/main/pg_hba.conf`
3. Create a linux user named 'catalog' for psql:   
`$ sudo adduser catalog` (choose a password)
4. Switch to default user postgres:   
`$ sudo su - postgre`
5. Connect to the psql system:   
`$ psql`
6. Create a postgre user named 'catalog':  
  1. Create user with LOGIN role and set a password:  
    `# CREATE USER catalog WITH PASSWORD 'password';` (# stands for the command prompt in psql)
  2. Allow the user to create database tables:  
    `# ALTER USER catalog CREATEDB;`
  3. *List current roles and their attributes:
    `# \du`
7. Create database:  
  `# CREATE DATABASE catalog WITH OWNER catalog;`
8. Connect to the database catalog
  `# \c catalog` 
9. Revoke all rights:  
  `# REVOKE ALL ON SCHEMA public FROM public;`
10. Grant only access to the catalog role:  
  `# GRANT ALL ON SCHEMA public TO catalog;`
11. Exit out of PostgreSQl and the postgres user:  
  `# \q`, then `$ exit` 

Sources: [Trackets Blog][15], [Super User][16]

##### 12. Install git, clone and set up your Flask web app

###### 1. Install git and clone repository
1. Install Git:  
`$ sudo apt-get install git`
2. Set your name, e.g. for the commits:  
`$ git config --global user.name "username"`
3. Set up your email address to connect your commits to your account:  
`$ git config --global user.email "me@email.com"`
4. Clone app repository from GitHub:  
  `$ git clone https://github.com/username/app.git`
5. Move all content of cloned repository `/var/www/catalog/catalog/` delete the empty directory
6. Make the repository inaccessible:  
  1. Create and open .htaccess file:  
    `$ cd /var/www/catalog/` and `$ sudo nano .htaccess` 
  2. Paste in the following:  
    `RedirectMatch 404 /\.git`

###### 2. set up your Flask web app
1. Open the database setup file:   
`$ sudo vim database_setup.py`
2 Edit the line starting with "engine" and fill in psql password for 'catalog' user:
`engine = create_engine('postgresql://catalog:password@localhost/catalog')`
3. Make the same change in `application.py`
4. 
2. Restart Apache:
`$ sudo service apache2 restart`
3. Visit public IP in web browser to check that app is running.

Sources: [GitHub][17], [Stackoverflow][18]

#### Additional Functionalities


[1]: https://github.com/robertozanchi/catalog-app
[2]: https://www.udacity.com/account#!/development_environment
[3]: https://www.udacity.com/account#!/development_environment
[4]: http://askubuntu.com/questions/94102/what-is-the-difference-between-apt-get-update-and-upgrade "What is the difference between apt-get update and upgrade?"
[5]: https://www.digitalocean.com/community/tutorials/additional-recommended-steps-for-new-ubuntu-14-04-servers
[6]: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps
[7]: http://askubuntu.com/questions/410244/a-command-to-list-all-users-and-how-to-add-delete-modify-users "How to list, add, delete and modify users"
[8]: http://askubuntu.com/questions/16650/create-a-new-ssh-user-on-ubuntu-server
[9]: https://www.udacity.com/course/viewer#!/c-ud299-nd/l-4331066009/m-4801089481
[10]: http://askubuntu.com/questions/16650/create-a-new-ssh-user-on-ubuntu-server
[11]: https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server
[12]: http://blog.udacity.com/2015/03/step-by-step-guide-install-lamp-linux-apache-mysql-python-ubuntu.html
[13]: https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
[14]: https://github.com/stueken/FSND-P5_Linux-Server-Configuration/blob/master/README.md
[15]: http://blog.trackets.com/2013/08/19/postgresql-basics-by-example.html "PostgreSQL Basics by Example"
[16]: http://superuser.com/questions/769749/creating-user-with-password-or-changing-password-doesnt-work-in-postgresql
[17]: https://help.github.com/articles/set-up-git/#platform-linux "Set Up Git for Linux"
[18]: http://stackoverflow.com/questions/6142437/make-git-directory-web-inaccessible "Make .git directory web inaccessible"
