---
title: Installation
layout: page
type: tute
---

This guide assumes a working knowledge on how to set up apache to serve a PHP application as well as having an empty MySQL database (with user and password) ready to go. For help in setting up a user and password see 'Creating MySQL Users' in the 'Help' menu.

First, you must install Cmfive's dependencies. 

For Windows:
- install [Docker Desktop](https://releases.ubuntu.com/18.04.5/?_ga=2.67351829.527945484.1625616788-786732526.1625616788) 
- install Ubuntu 18.04

For Mac and Linux:
- install Docker

Install VSCode. This is needed for all operating systems.

To install Cmfive, clone or download [the Boilerplate repository](https://github.com/2pisoftware/cmfive-boilerplate) and unpack (if necessary) into a directory of your choosing.
<br>
If you are using Windows it will need to be cloned to ubuntu partition.

Open the Boilerplate repository in VSCode and locate the docker-compose.yml file (near the bottom). Right click it and choose compose-up. The terminal will automatically run through several things. This may take several minutes.

Next you need to set up a MySQL user. If you are unsure how to do this, click [here](/tutorials/help_module/mysql-users) for instructions.

Copy the config.php.example file to config.php and update the database section to contain the credentials of your Cmfive database. The user, password, and database should all be "cmfive", the host is mysql-5.7 and the port is 3306, e.g.:
```php
Config::set("database", [
    "hostname"  => "localhost",
    "username"  => "cmfive",
    "password"  => "cmfive",
    "database"  => "cmfive",
    "driver"    => "mysql"
]);
```
The system environment section of this file should be set ot development.

Change any other configuration items as you see fit (You will need to purge the config cache after changing configuration files. This is done by deleting the config item for encryption). 

Attach a shell to the cmfive-boilerplate container. To do this go to the docker tab in VSCode:

![Docker Tab](/assets/images/docker.png)

Right click the cmfive-boilerplate container (Under CONTAINERS and cmfive-boilerplate. The one called cmfive-boilerplate_webapp) and choose attach shell.

Type the below command into the terminal.
```sh
php cmfive.php
```
Running through commands 1-4 will get you set up and ready to go. Here is an explanation of each command.
1. Will install any third party libraries Cmfive requires via Composer (the composer executable is bundled with the Boilerplate repo).
2. Will install all Cmfive migrations.
3. Will set up an administrator user, needed to log in to a new Cmfive install.
4. Will generate encryption keys used by Cmfive.

Open a new VSCode window that does not have a repository open in it. Go to the terminal. Choose View an Terminal from the toolbar menu if it does not automatically appear at the bottom of your new menu. This terminal should not be attached to any container, so it should have the name of your computer and no repository name after it.

In this terminal run the following commands one at a time:
```sh
sudo chmod 777 -R storage/
sudo chmod 777 -R cache/
```
If you get an error, try removing sudo and running the commands again.

Open Cmfive in your browser to check it is working. You should see a page like this:

![Login Page](/assets/images/cmfive_login.png)

Make sure you can login and see the main index bar. If there are issues with this, check some of the commands under MySQL Users in the Database below to make sure the correct user is set, and has all their permissions.

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