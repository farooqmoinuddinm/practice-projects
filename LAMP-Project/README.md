# Setting up the LAMP Server in Ubuntu.
### Created the ec2-instance in AWS cloud.
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/65aedfba-42ab-41cc-ab43-f3cd0f532f8d">
### Logged into the server and installed the LAMP packages with below commands.\

*apache2 installation*


```

# Update the system packages
sudo apt update
# Install the apche server
sudo apt install apache2
 

```
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/fa856265-d8fe-4088-8be1-3272cf3c9dd7">

*mysql server installation*
```

# Install the mysql server
sudo apt install mysql-server -y
# Login to the mysql server
sudo mysql
# Secure the mysql installation
sudo mysql_secure_installation

```
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/1347e487-4aaa-415f-8724-eaf669a1c0e4">
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/c23208ef-0c47-44ae-8bbc-585e4192954d">

*PHP installation*
```

sudo install php libapache2-mod-php php-mysql
php -v
sudo vim /var/www/html/index.php
# Below code to the above index.php file to check the php installation.
<?php
phpinfo();

sudo rm -rf /var/www/html/index.html
# also remove the index.php file once the testing is completed as it has the sensitive information.
sudo rm -rf /var/www/html/index.php

```
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/8da8b25a-fe19-4696-aa24-7e0d27c3123c">\

<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/4661e64f-2a9c-4c1d-8ed0-02007ab0f140">

#### Creating virtual hosting for the website.

```
# Creaet a project Directory
sudo mddir /var/www/projectlamo
# Change the owner of the directory to logged in user
sudo chown $USER:$USER /var/www/projectlamp
# Create site conf file and add the conf data to it.
sudo vi /etc/apache2/sites-available/projectlamp.conf

<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

# Check the file is created.
sudo ls /etc/apache2/sites-available/

# Enabled the created the virtual site
sudo a2ensite projectlamp
# Disabled the default site
sudo a2dissite 000-default.conf

# Finally reload the apache
systemctl reload apache2

# Create test data with below command for projectlamp.
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html

```
<img width="452" alt="image" src="https://github.com/farooqmoinuddinm/practice-projects/assets/23025815/5cda8bad-0e42-433c-a822-a2f757e6d593">
