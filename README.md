# Linux Server Setup

## Project Overview
This is project #5 of **Udacity's Full Stack Web Developer Nanodegree**.
The main task is to configure a baseline installation of Ubuntu Linux
on a virtual machine, and use it host a [Flask web application][1] 
developed earlier in the course. Udacity provided the Amazon AWS development
environment for this project.

## Hosted Web App

The deployed web application can be accessed at
http://ec2-54-148-92-221.us-west-2.compute.amazonaws.com/. 

The use of a web browser such as Google Chrome in "incognito" mode is recommended.

## Server Login

The Udacity reviewer may log into the server as the 'grader' user
at the public IP address 54.148.92.221 and using SSH port 2200. The
key is provided in Notes for Reviewer below.

SSH into the server as 'grader' with: ssh -i ~/.ssh/udacity grader@54.148.92.221 -p 2200

## Step by Step Installation
This section outlines the different stages of installation. Its two parts
are **Basic Setup and Deployment of Web App**, which presents how the project
meets the basic Udacity requirements, and **Additional Functionalities**, 
which describes the steps taken to exceed minimum specifications. Links to 
third-party resources used are also included in this section. 

### Basic Setup and Deployment of Web App

#### 1. Access to the development environment
The Amazon AWS development environment is available to Udacity Full Stack
Development Nanodegree students through their [Udacity account][2].

The public IP address of the virtual machine created and used in this project
is 54.148.92.221.

#### 2. SSH into server as root user
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

#### 3. Create a new user named grader
The steps to create a new user named grader are:

1. 

Sources: [Digital Ocean][4]


### Additional Functionalities

## Notes for Reviewer

[1]: https://github.com/robertozanchi/catalog-app
[2]: https://www.udacity.com/account#!/development_environment
[3]: https://www.udacity.com/account#!/development_environment
[4]: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps
