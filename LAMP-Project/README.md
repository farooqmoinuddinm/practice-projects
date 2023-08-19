# Setting up the LAMP Server in Ubuntu.

#### What is LAMP ?
LAMP is an acronym that represents a popular software stack used for building and deploying web applications. It stands for: Linux, Apache, MYSQL and PHP.\
In the this project I will be setting up the Ubuntu machine in AWS public cloud to deploy this popular web application stack.

#### Here is the EC2 intance created in AWS account for LAMP server.
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/65aedfba-42ab-41cc-ab43-f3cd0f532f8d">

#### Before you install any software, you need to update system packages with below commands

```
sudo apt update -y
```
#### Install the apche2 web server package with below command
```
sudo apt install apache2 
```
#### make sure that service should be running, below is the command for to check the service status
```
sudo systemctl status apache2
```
#### you can check accessing the web page with your public ip or dns name and below is the screenshot of the web server
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/fa856265-d8fe-4088-8be1-3272cf3c9dd7">

#### Now we need to install the MYSQL Database server, run the below command to install mysql-server
```
sudo apt install mysql-server -y
```
#### Login to mysql server and check if the installation success or not. 
```
sudo mysql
```
#### Here is the screenshot of the mysql login.
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/1347e487-4aaa-415f-8724-eaf669a1c0e4">\

#### By default mysql server is not secure, we need to secure it running the below command.
```
sudo mysql_secure_installation
```
#### You need to run through the mysql secure prompt.
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/c23208ef-0c47-44ae-8bbc-585e4192954d">


#### We have complleted Database installation, in next step we need to install the PHP and its dependent packages with below command.
```
sudo install php libapache2-mod-php php-mysql
```
#### check php version running the below command.
```
php -v
```
#### Here is the screenshot of the php version.
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/b58d64e9-8e47-45b3-8d6f-ce4ef2ca14c2">

#### Create a index.php file in /var/www/html directory
```
sudo vim /var/www/html/index.php
```
#### Add the below code to the index.php file and access through the browser to check our php installation is working.
```
<?php
phpinfo();
```
#### We can see that PHP details from the browser.
<img width="1500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/4661e64f-2a9c-4c1d-8ed0-02007ab0f140">

### We have successfully installed the LAMP in ubuntu server, let's take it further configuring the virtual sites in apache.

#### Let's create a project for virtual hosting in apache server
#### Create a project directory in /var/www/
```
sudo mkdir /var/www/projectlamp
```
#### Change the owner of the current logged in User
```
sudo chown $USER:$USER /var/www/projectlamp
```
#### We also need to create a config file for our projectlamo in /etc/apache2/sites-available/projectlamp.conf
```
sudo vi /etc/apache2/sites-available/projectlamp.conf
```
#### Add the below code to the site config file projectlamp.conf
```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
#### Make sure that site conf file is created, run below command to check.
```
sudo ls /etc/apache2/sites-available/
```
#### you also need to enable the virtual site with below command
```
sudo a2ensite projectlamp
```

#### Make sure to disable the default site with below command.
```
sudo a2dissite 000-default.conf
```
#### We have added the config data, we need to reload the apache service with below command
```
systemctl reload apache2
```

#### Add some sample data to our project index.html file using following command.
```
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
```
#### Here is the application you can see accessing from the browser for your virtual site 
<img width="2500" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/44595243-9e4a-4f00-86c6-832b8ca3e044">

