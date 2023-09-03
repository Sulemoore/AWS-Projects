## Installation should be done on both App servers.

- To ensure that all of your software packages are up to date, perform a quick software update on your instance.
```
sudo yum update -y
```

- Install the lamp-php7.2
```
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
```

- View your version of Amazon Linux to make sure there was no errors
```
cat /etc/system-release
```

- Install the Apache web server and PHP software packages.
```
sudo yum install -y httpd
```

- Start the Apache web server.
```
sudo systemctl start httpd
```

- Use the systemctl command to configure the Apache web server to start at each system boot.
```
sudo systemctl enable httpd
```

- You can verify that httpd is on.
```
sudo systemctl is-enabled httpd
```

- Add your user (in this case, ec2-user) to the apache group.
```
sudo usermod -a -G apache ec2-user
```

- Log out and then log back in again to pick up the new group, and then verify your membership.
```
exit
```
```
ssh -i "mykeypair.pem" ec2-user@10.0.5.151
```

- verify your membership in the apache group
```
groups
```

- Change the group ownership of /var/www and its contents to the apache group.
```
sudo chown -R ec2-user:apache /var/www
```

- Add group write permissions and to set the group ID on future subdirectories, change the directory permissions of /var/www and its subdirectories.
```
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
```
- Add group write permissions, recursively change the file permissions of /var/www and its subdirectories:
```
find /var/www -type f -exec sudo chmod 0664 {} \;
```
```
sudo yum list installed httpd php-mysqlnd
```

- Delete the phpinfo.php file.
```
rm /var/www/html/phpinfo.php
```

### Install phpMyAdmin
- Install the required dependencies.
```
sudo yum install php-mbstring php-xml -y
```

- Restart Apache.
```
sudo systemctl restart httpd
```

- Restart php-fpm
```
sudo systemctl restart php-fpm
```

- Navigate to the Apache document root at `/var/www/html`
```
cd /var/www/html
```

- Download the latest phpMyAdmin release
```
wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
```

- Create a phpMyAdmin folder and extract the package into it
```
mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1
```

- Delete the phpMyAdmin-latest-all-languages.tar.gz tarball.
```
rm phpMyAdmin-latest-all-languages.tar.gz
```



```

After Database has been configured

```
cd /var/www/html
mv config.sample.inc.php config.inc.php
vi config.inc.php
```
