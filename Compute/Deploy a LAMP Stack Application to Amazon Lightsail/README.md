# Deploy a LAMP Stack Application to Amazon Lightsail 📌

In this project, we will deploy a LAMP (Linux Apache MySQL PHP) stack application onto a single Lightsail instance.

- Amazon Lightsail is one of the easiest ways to get started on AWS. It offers virtual servers, storage, databases, and networking, plus a cost-effective, monthly plan.

-At the end of this project, you will have a solid understanding of how to use Lightsail to quickly stand up a multi-tier web application.

## Step 1: Create an Amazon Lightsail account


## Step 2: Create an Amazon Lightsail instance

1. Choose Create instance on the Instances tab of the Lightsail homepage.
2. An AWS Region and Availability Zone is selected for you. Choose Change AWS Region and Availability Zone to create your instance in another location.
3. Retain Linux/Unix as the platform and under Select a blueprint choose LAMP (PHP 7).

## Step 3: Install the application code
In this section, you use a launch script to install the demo application. Launch scripts run the first time an instance boots up, and are used to do any initial configuration on an instance. 

1. Choose +Add launch script.
2. Paste the script below into the launch script text window.
-The script performs the following actions:

-Removes the default Apache website
-Clones the application code from GitHub into the htdocs directory
-Ensures the configuration file is writeable
-Uses sed to read the local database password from a file on the disk and insert it into the configuration file
-Runs an SQL script to set up the application’s database

```
# remove default website
#-----------------------
cd /opt/bitnami/apache2/htdocs 
rm -rf *

# clone github repo
#------------------
git clone -b loft https://github.com/mikegcoleman/todo-php .

# set write permissions on the settings file
#-----------------------------------
sudo chown bitnami:daemon connectvalues.php
chmod 666 connectvalues.php

# inject database password into configuration file
#-------------------------------------------------
sed -i.bak "s/<password>/$(cat /home/bitnami/bitnami_application_password)/;" /opt/bitnami/apache2/htdocs/connectvalues.php

# create database
#----------------
cat /home/bitnami/htdocs/data/init.sql | /opt/bitnami/mariadb/bin/mysql -u root -p$(cat /home/bitnami/bitnami_application_password)

```
3. Choose the free tier instance plan.

4. Enter a name for your instance and choose Create instance.
Resource name guidelines:

--Must be unique within each AWS Region in your Lightsail account.
-Must contain 2 to 255 characters.
-Must start and end with an alphanumeric character or number.
-Can include alphanumeric characters, numbers, periods, dashes, and underscores.

## Step 4: Test the Application
1. a. It will take 2-3 minutes for your instance to start up. Once the status is listed as Running, move on to the next step.
 
-Note: You may need to refresh your web browser to see the updated status.

2. Make note of your instance’s IP address.

3. In your web browser, navigate to the instance’s IP address. You should see the application running.

## Step 5: Clean up

1. On the Instances tab of the Lightsail home page, choose the ellipsis (⋮) icon next to the LAMP instance you just created and choose Delete.
2. Select Yes, delete from the prompt.

# Conclusion
Congratulations! You used Amazon Lightsail to run a LAMP stack application.

Amazon Lightsail is great for developers, web pros, and anyone looking to get started on AWS quickly and cheaply. You can launch instances, databases, and SSD-based storage; transfer data; monitor your resources; and so much more in a managed way.