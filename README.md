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

The Udacity reviewer may log into the server as the 'grader' user
at the public IP address 54.148.92.221 and using SSH port 2200. The
key is provided in Notes for Reviewer below.

SSH into the server as 'grader' with: ssh -i ~/.ssh/udacity grader@54.148.92.221 -p 2200

### Step by Step Installation
This section outlines the different stages of installation. Its two parts
are **Server Setup and Deployment of Web App**, which presents how the project
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

Sources: [Udacity][3]

##### 3. Update all currently installed packages
The steps to update the packages installed on the server are:

1. Update the list of available packages and their versions:  
  `$ sudo apt-get update`
2. Install newer vesions of packages you have:  
  `$ sudo sudo apt-get upgrade`

Sources: [Ask Ubuntu][4]

##### 3. Create new user 'grader' with sudo permission
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

Sources: [Ask Ubuntu][6], [Ask Ubuntu][7], [Digital Ocean][5]

##### 5. Enable key based authentication for grader

1. Generate a SSH key pair on the local machine:  
  `$ ssh-keygen`
2. Confirm the file path and name for new key pair:  
   For example `$ /Users/Udacity/.ssh/udacity`
3. Optionally, enter a passphrase for the new key pair
4. Log in as grader and create .ssh directory in home directory:  
   `$ mkdir .ssh`
5. 

##### 6. Change the SSH port from 22 to 2200 and disable root
The steps to change SSH port to 2200 and disable root user are:




#### Additional Functionalities

### Resources

### Notes for Reviewer

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEA9DYmh/4XiDnzXtTzFBbKlkzLrdVQMYRsCKUvErakYikZJ7cr
AKG/T+DHWBZXRXCCFxiNbEt5EnHOOj35QsqQ5R1WB2BRQ8Q6ODZ94IM6LQ9GjsqB
rXAg4s5oDxFg4FGIfQ+Yo9yViIrUS3fkeZ267Xj0PoLJw3Sq++gBuEnkSMQ5YuYn
Cx7/Jj6GI8i0ya6RgVG72wZYJTlWxe24bVuoLrA0Fn7RYoHGGdYUaCqUSo8n27SW
kj0Sv8JckJDUBDPvRoZSiYX3EMrL9u9BnPT40Bi7L8IZpeoqvZddWtdDOsvcI8dj
3N/DWRTVgkiE4hPllEl/2yIVJuZz30X8q36NbQIDAQABAoIBAHLcJTNBJwBDgVvQ
/KMuNQqMBCA2fAlOJyHJz2IV1Sr1+Ybcd7VMXhbLufaMS2+1gvop6hpNRRyPulda
XqozbALW0WeWvaIJ4PgfaQT3s50N2jm+tU9FtbH3MqojmlTnBDMN6tTnIs2dvkvg
j+1Dam/Wu8nK6eqsLN9eN7Dd0CkIdl4UKP+6FMQtJl4VdWQi8VmEyUI2I9fOfq4K
UeHZP5d4Es4ZqtBoJ/CyGa49h9J6WTWkpaxwru6mwR2k2lyffYWE1Hp+S01zE2yH
T3QgO2fAZ7vpBYEJyZNSTrPGuTYPZX8+111gvoZsZ/Z+rNfH+aNizlxXDLXgNT76
wmiiDWECgYEA/KdZrG4fEI4HBCOvQTAvDUXKKX2kW+N3jev3daQLqKYSLfaPgGS6
wiDC1P/L7jm190iMJBCzJevftbO7zyI/VQF2B2ffK9C0e3exC4qW8MrnZR9MWlh3
Vz9OJVYO5cd6N5ofxUaCHbREyFWZtxp/YXp0QrOSZ4SoovJYMm6onN8CgYEA93It
E4eld62pXilT9TbUUSsRSEpiqnvwxX3di5Jn1ruDsbFFrtsz+iHrfuxUXcbyeTIa
u5U4G3mtPA3iCqabjYmtrWeGdINF8icvXJRUd7V/V9KHrL+I7fYMV2UlAoS4uxKf
IGElI5/OI1eMjwFHKoJxGMBmE7a7Km3kaQFVUzMCgYBeHoGbaJKN+jrG4fxBjo+Y
pC0Bc9qsmHpLFmJjIq9tLiCLmtQuglfIRagO7ROtNTaCXjZGoSn7sHjwGXqXWSy6
oAa2D43lpqP1csszf3dnUE8PLq+k4Fvk1qJn6j02gC8ZU4MOXIvQQP12m9zdhzN4
vsNcrcSWZ6bivOD6OJr7hQKBgBvEKh645+5oBEtWo98uSeDZzlSoVC4BPmFK4GNb
CF/mJr73v3QBkPGOgNh7OHRVcLv8zVcjRWp/2tqUTDsZuvbE7kI5DbNhT6X+k6f1
1QyhxypZq3PNAlaBd50O8no33mrPih+eBwbaVc1Nc65QXGX+wSYf4NRxessmDa1i
wupVAoGADL4euxwfp8eC/z58RjeMV076xLUgChunkVZ+vW9s23qG/mLsFNRBPFMq
VXLCjck12Qgmy1BrHM9XFTBpX5ttFcz1pVqfzxAibuOMFgQ6Gs8AL2sm+16rlqcn
Kh3v5AsFgUZp6tYrUDPIYeNZ4/va2cjIUy5JD8tCivVMpxrjG30=
-----END RSA PRIVATE KEY-----

[1]: https://github.com/robertozanchi/catalog-app
[2]: https://www.udacity.com/account#!/development_environment
[3]: https://www.udacity.com/account#!/development_environment
[4]: http://askubuntu.com/questions/94102/what-is-the-difference-between-apt-get-update-and-upgrade "What is the difference between apt-get update and upgrade?"
[5]: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps
[6]: http://askubuntu.com/questions/410244/a-command-to-list-all-users-and-how-to-add-delete-modify-users "How to list, add, delete and modify users"
[7]: http://askubuntu.com/questions/16650/create-a-new-ssh-user-on-ubuntu-server
