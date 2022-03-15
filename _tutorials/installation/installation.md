---
title: Installation
layout: page
type: tute
---

## Installing Cmfive for Local Development

First, you must install Cmfive's dependencies. 

For Windows:
- install [Docker Desktop](https://releases.ubuntu.com/18.04.5/?_ga=2.67351829.527945484.1625616788-786732526.1625616788) 
- install Ubuntu 18.04

For Mac and Linux:
- install Docker

## Installation using VS Code

1. Install VSCode. This is needed for all operating systems.

2. To install Cmfive, clone or download [the Boilerplate repository](https://github.com/2pisoftware/cmfive-boilerplate) and unpack (if necessary) into a directory of your choosing.
<br>
If you are using Windows it will need to be cloned to ubuntu partition.

3. Open the Boilerplate repository in VSCode.

4. Install the Docker extension specified in [requirements](/tutorials/installation/requirements) in VS Code.

5. Locate the docker-compose.yml file (near the bottom). Right click it and choose compose-up. The terminal will automatically run through several things. This may take several minutes.

6. When Docker Compose has finished, check that you have three containers running by clicking on the Docker tab on the left.

![Docker Tab](/assets/images/docker.png)

7. Next you need to set up a MySQL user. If you are unsure how to do this, click [here](/tutorials/help_module/mysql-users) for instructions.

8. Connect to MySQL by right clicking on the MySQL container (labelled mysql:5.7.21 or similar) in the Docker tab and choosing ```Attach Shell```. Then type ```mysql -u root -p``` with the password ```root```.

9. Run the following commands:
 - ```CREATE DATABASE cmfive;```
 - ```CREATE USER cmfive@'%' IDENTIFIED BY 'cmfive';```
 - ```GRANT ALL PRIVILEGES ON cmfive.* TO cmfive@'%';```
 - ```FLUSH PRIVILEGES;```

You can now close the terminal window to the MySQL Container. l

10. Copy the ```config.php.example``` file to ```config.php```. Replace ```<username>```, ```<password>``` and ```<database>``` with ```cmfive```.

Also replace ```localhost``` with the _name_ of your MySQL container, usually ```mysql-5.7``` or ```mysql-8``` depending on the version of Cmfive you are using. The port should be ```3306```.

The system environment section of this file should be set ot development.

11. Change any other configuration items as you see fit (You will need to purge the config cache after changing configuration files. This is done by deleting the config item for encryption). 

I.e. remove this if present:
 ```php
 Config::set('system.encryption', [
     'key' => '',
     'iv'  => ''
 ]);
 ```

12. Open up a normal terminal window in VSCode. If you closed the terminal window when you closed the MySQL terminal above, there should be a small screwdriver and wrench symbol at the bottom blue bar of your window on the left. Clicking on this will re-open the terminal.<br>
To return the MySQL terminal to a normal terminal window look at the small menu on the right of the terminal window. There should be a wrench and screwdriver symbol with the name of your container next to it. If you hover over the name of the container a trash can symbol should appear. Clicking on this will return you to the normal terminal.

![Closing the MySQL Terminal](/assets/images/closing_mysql_shell.png)

In the terminal window run ```chmod 777 -R cache/ storage/ uploads/```

13. Attach a shell to the cmfive-boilerplate container. To do this go to the docker tab in VSCode.

Right click the cmfive-boilerplate container (Under CONTAINERS and cmfive-boilerplate. The one called cmfive-boilerplate_webapp) and click ```Attach Shell```.

14. Type the below command into the terminal.
```sh
php cmfive.php
```
15. Running through commands 1-4 will get you set up and ready to go. Here is an explanation of each command:
    1. Will install any third party libraries Cmfive requires via Composer (the composer executable is bundled with the Boilerplate repo).
    2. Will install all Cmfive migrations.
    3. Will set up an administrator user, needed to log in to a new Cmfive install.
    4. Will generate encryption keys used by Cmfive.

16. Open a new VSCode window that does not have a repository open in it. Go to the terminal. Choose View an Terminal from the toolbar menu if it does not automatically appear at the bottom of your new menu. This terminal should not be attached to any container, so it should have the name of your computer and no repository name after it.

17. In this terminal run the following commands one at a time:
```sh
sudo chmod 777 -R storage/
sudo chmod 777 -R cache/
```
If you get an error, try removing sudo and running the commands again.

To check it is working, open Cmfive in your browser, by right clicking the boilerplate container in the docker tab and clicking ```Open in browser```. You should see a page like this:

![Login Page](/assets/images/cmfive_login.png)

17. Make sure you can login and see the main index bar. If there are issues with this, open up your ```config.php``` file and append the following at the end of the file:
 ```php
 Config::set('system.environment', 'development');
 ``` 

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

## Installation using CLI

1. Clone the [Cmfive Boilerplate](https://github.com/2pisoftware/cmfive-boilerplate) repository using Git and navigate to it in your terminal of choice.

2. Run ```docker-compose up``` (This will take a while).

3. Check that you have 3 containers using ```docker ps```.

4. Connect to the database container by running ```docker exec -it mysql-5.7 bash``` (you will need to replace "5.7" with "8" if you are using Cmfive v5+). Connect to MySQL in the container by running ```mysql -u root -p``` with password ```root```.

5. un the following commands:
 - ```CREATE DATABASE cmfive;```
 - ```CREATE USER cmfive@'%' IDENTIFIED BY 'cmfive';```
 - ```GRANT ALL PRIVILEGES ON cmfive.* TO cmfive@'%';```
 - ```FLUSH PRIVILEGES;```

 You can now close the terminal window to this container or run ```exit``` twice to get back to your local CLI.

6. Copy the ```config.php.example``` file to ```config.php``` and replace ```<username>```, ```<password>``` and ```<database>``` with ```cmfive```. Also replace "localhost" with the _name_ of your MySQL container, usually ```mysql-5.7``` or ```mysql-8``` depending on the version of Cmfive you are using.

7. While you are in the config, if the ```system.encryption``` config key exists, remove it. I.e. remove this if present:
 ```php
 Config::set('system.encryption', [
     'key' => '',
     'iv'  => ''
 ]);
 ```

8. In your terminal window and run ```chmod 777 -R cache/ storage/ uploads/```.

9. Connect to the PHP webserver container by running ```docker exec -it nginx-php7.4 bash``` (you will need to replace "7.4" with "8.1" if you are using Cmfive v5+).

10. Run the following commands:
 - ```php cmfive.php install core```
 - ```php cmfive.php install migrations```
 - ```php cmfive.php seed encryption```
 - ```php cmfive.php seed admin Admin Admin <your email> admin admin```
     - This will make an admin user with username and password ```admin```. If you do not want this instead run ```php cmfive.php```, enter option 3 and follow the prompts.

11. Make sure you remove any log files under ```./storage/log```.

12. Run ```docker run -e 3000:3000``` and in your browser go to [http://localhost:3000/](http://localhost:3000/).

 If all has gone well then you should see a login screen! But you'll notice you cannot log in, we have one more step to do.

13. Open up your ```config.php``` file and append the following at the end of the file:
 ```php
 Config::set('system.environment', 'development');
 ```

 You should now be able to log in.