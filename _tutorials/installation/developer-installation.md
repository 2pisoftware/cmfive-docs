---
title: Further Installation for Deevelopers
layout: page
type: tute
---

If you are a developer these instructions will be needed in conjunction with those in [Installation](installation). Otherewise you may go onto the next steps by clicking next.

<!--finding hostname-->
Go to your docker-compose.yml file in the boilerplate. At around line 9, under mysqldb, their should be a hostname. Copy the name.<!--insert image of VSCode showing hostname-->

![hostanme in docker-compose.yml file](/assets/images/find_hostname.png)

In your config.php file, scroll down to Database Configuration. On the line specifying the hostname (the second line of code under Database Comfiguartion) change localhost to the hostname you copied. It should look something like this. <!--php code eaxmple-->

![hostname in config.php file](/assets/images/config_hostname.png)

Save the file and purge the cache by deleting the config.cache file. Purging the cache is explained further in Creating a Config under Learning Cmfive.
<!--creating user with found ip address-->