# Linux Server Setup
## Udacity Full Stack Web Developer Nanodegree

### Project Overview
This is project #5 of Udacity's Full Stack Web Developer Nanodegree.
The main task is to configure a baseline installation of Ubuntu Linux
on a virtual machine and use it host the [catalog application][1] 
developed earlier in the course using the Flask framework. Udacity
provided the Amazon AWS development environment for this project.

### The Hosted Web Application

The deployed web application can be accessed at
http://ec2-54-148-92-221.us-west-2.compute.amazonaws.com/. 

A web browser such as Google Chrome in "incognito" mode is recommended.

### Log into the server

The Udacity reviewer may log into the server as the 'grader' user
at the public IP address 54.148.92.221 and using SSH port 2200. The
key is provided in Notes for Reviewer below.

ssh -i ~/.ssh/udacity grader@54.148.92.221 -p 2200

### Step by Step Installation
This section outlines the different stages of installation. Its two parts
are 'Basic Setup and Deployment of Web App', which presents how the project
meets the basic Udacity requirements, and 'Additional Functionalities', 
which describes the steps taken to exceed minimum specifications. Links to 
third-party resources used are also included in this section. 

#### Basic Setup and Deployment of Web App

##### 0. Access to the Development Environment
The Amazon AWS development environment is available to Udacity Full Stack
Development Nanodegree students as part of the [account][2].

The public IP address of the virtual machine created and used in this project
is 54.148.92.221.

##### 1. SSH into Server as Root User
In step 1 the Ubuntu Linus server is accessed as root user.
1. Note public IP address of virtual machine: 54.148.92.221.
2. 

1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][3].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID.

#### 2.

#### Additional Functionalities

### Notes for Reviewer

[1]: https://github.com/robertozanchi/catalog-app
[2]: https://www.udacity.com/account#!/development_environment

