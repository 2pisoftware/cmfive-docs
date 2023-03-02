---
title: Installation
layout: page
type: tute
---

## Installing Cmfive for local development:

## Installation Requirements
- Docker
- Docker Compose
- Git

###### **TIP** If you're on **Windows** your life will be made easier by also having WSL (preferably WSL2)

## Setup steps using **VS Code**
###### See below for install steps using CLI

#### Step 1 - Getting the code
Clone the [Cmfive Boilerplate](https://github.com/2pisoftware/cmfive-boilerplate) repository using Git and open the cmfive-boilerplate folder in VS Code

#### Step 2 - Installing Docker extension
Install the Docker extension by Microsoft (extension ID: ```ms-azuretools.vscode-docker```)

#### Step 3 - Building the containers
Right-click on the ```docker-compose.yml``` file and select ```Compose Up``` (This will take a while)

#### Step 4 - Verify
When docker compose has finished, check that you have 3 containers ready by clicking on the Docker tab on the left
![Docker Tab](/assets/images/docker.png)

#### Step 5 - Connect to database container
Right click on the MySQL container and click ```Attach Shell```. Connect to MySQL in the container by running ```mysql -u root -p``` with password ```root```

#### Step 6 - Create database and database user
Run the following commands:
- ```CREATE DATABASE cmfive;```
- ```CREATE USER cmfive@'%' IDENTIFIED BY 'cmfive';```
- ```GRANT ALL PRIVILEGES ON cmfive.* TO cmfive@'%';```
- ```FLUSH PRIVILEGES;```

You can now close the terminal window to this container

#### Step 7 - Prepare Cmfive config
Copy the ```config.php.example``` file to ```config.php``` and replace ```<username>```, ```<password>``` and ```<database>``` with ```cmfive```. Also replace ```localhost``` with the _name_ of your MySQL container, usually ```mysql-5.7``` or ```mysql-8``` depending on the version of Cmfive you are using

While you are in the config, if the ```system.encryption``` config key exists, remove it. I.e. remove this if present:
```php
Config::set('system.encryption', [
    'key' => '',
    'iv'  => ''
]);
```
The system environment section of this file should be set to development.

```php
Config::set('system.environment', 'development');
```

#### Step 8 - Connect to PHP container
Right click on the ```nginx-php``` container and click ```Attach Shell```.

#### Step 9 - Make directories accessible to containers
In the container run ```chmod 777 -R cache/ storage/ uploads/```

#### Step 10 - Install Cmfive
Run the following commands:
- ```php cmfive.php install core```
- ```php cmfive.php seed encryption```
- ```php cmfive.php install migrations```
- ```php cmfive.php seed admin Admin Admin <your email> admin admin```
    - This will make an admin user with username and password ```admin```. If you do not want this instead run ```php cmfive.php```, enter option 3 and follow the prompts

#### Step 11 - Open!
Make sure you remove any log files under ```./storage/log```.

Right click on the ```nginx-php``` container in the Docker extension tab and click ```Open in browser```

If all has gone well then you should see a login screen! But you'll notice you cannot log in, we have one more step to do

#### Step 12 - Turn on development mode
Open up your ```config.php``` file and append the following at the end of the file:
```php
Config::set('system.environment', 'development');
```

You should now be able to log in

## Setup steps using CLI
#### Step 1 - Getting the code
Clone the [Cmfive Boilerplate](https://github.com/2pisoftware/cmfive-boilerplate) repository using Git and navigate to it in your terminal of choice

#### Step 2 - Building the containers
Run ```docker-compose up``` (This will take a while)

#### Step 3 - Verify
Check that you have 3 containers using ```docker ps```

#### Step 4 - Connect to database container
Connect to the database container by running ```docker exec -it mysql-5.7 bash``` (you will need to replace "5.7" with "8" if you are using Cmfive v5+). Connect to MySQL in the container by running ```mysql -u root -p``` with password ```root```

#### Step 5 - Create database and database user
Run the following commands:
- ```CREATE DATABASE cmfive;```
- ```CREATE USER cmfive@'%' IDENTIFIED BY 'cmfive';```
- ```GRANT ALL PRIVILEGES ON cmfive.* TO cmfive@'%';```
- ```FLUSH PRIVILEGES;```

You can now close the terminal window to this container or run ```exit``` twice to get back to your local CLI

#### Step 6 - Prepare Cmfive config
Copy the ```config.php.example``` file to ```config.php``` and replace ```<username>```, ```<password>``` and ```<database>``` with ```cmfive```. Also replace "localhost" with the _name_ of your MySQL container, usually ```mysql-5.7``` or ```mysql-8``` depending on the version of Cmfive you are using

While you are in the config, if the ```system.encryption``` config key exists, remove it. I.e. remove this if present:
```php
Config::set('system.encryption', [
    'key' => '',
    'iv'  => ''
]);
```

#### Step 7 - Connect to PHP container
Connect to the PHP webserver container by running ```docker exec -it nginx-php7.4 bash``` (you will need to replace "7.4" with "8.1" if you are using Cmfive v5+)

#### Step 8 - Make directories accessible to containers
In the container, run ```chmod 777 -R cache/ storage/ uploads/```

#### Step 9 - Install Cmfive
Run the following commands:
- ```php cmfive.php install core```
- ```php cmfive.php seed encryption```
- ```php cmfive.php install migrations```
- ```php cmfive.php seed admin Admin Admin <your email> admin admin```
    - This will make an admin user with username and password ```admin```. If you do not want this instead run ```php cmfive.php```, enter option 3 and follow the prompts

#### Step 10 - Open!
Make sure you remove any log files under ```./storage/log```.

Run ```docker run -e 3000:3000``` and in your browser go to [http://localhost:3000/](http://localhost:3000/)

If all has gone well then you should see a login screen! But you'll notice you cannot log in, we have one more step to do

#### Step 11 - Turn on development mode
Open up your ```config.php``` file and append the following at the end of the file:
```php
Config::set('system.environment', 'development');
```

You should now be able to log in

## Trouble Shooting 

If you still have trouble logging in, check some of the commands under MySQL Users in the Database below to make sure the correct user is set, and has all their permissions.

Please check out the Help pages for further support. Some operating systems may run into further issues and we can't always offer support.

## MySQL Users in the Database

The following command will show you the change owner options.
```bash
chown --help
```

To change the owner and group for all of the files:
```bash
chown -R www-data:www-data storage/
```

Copy the following bash commands into your terminal one at a time and click enter.

```bash
use cmfive;
```

```bash
MySQL> select * from user;
```

The ‘*’ means ‘all’, so you are asking to see all the information on the current user. 

The output will give you a table of information about the user. 

