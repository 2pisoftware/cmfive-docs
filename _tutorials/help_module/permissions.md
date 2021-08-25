---
title: Permissions Error
layout: page
type: tute
---

## Permissions Error - I Can't Log In

<!--check logs-->
In the files tab go to /system/log. The log files record any errors that users encounter and can help us to see when they are cropping up. How to read the entries in the log files is explianed in the the [logs help page](logs).<br>
The last file in the logs folder will have todays date. This is the one you want to check for the errors you just encountered. The most recent activtiy will be at the bottom of this file.
<!--system/modules/auth/actions/login.php ha important info on logging in-->

<!--Using inspect in Firefox. Look up for Windows and Linux as well as Mac-->
Now we need to inspect the element.<br>
Firefox users right click and choose Inspect at the bottom of the pop-up.<br>
Safari users right click and choose Inspect Elemment at the bottom of the pop-up.

<!--delete config cache after changing config-->
You will need to purge the config cache after making changes to the configuration file. you can see how to do this on the Creating a Config page under the Learning Cmfive menu.

<!--attach shell to boilerplate-->
Click on this tab on the left hand side of VSCode.<br>
![Docker tab](/assets/images/docker.png)<br>
Right click on the container called cmfive-boilerplate and select attach a shell. The VSCode terminal at the bottom of the screen is now a cmfive-boilerplate bash shell.
<!--Get mkcert
https://kifarunix.com/how-to-create-self-signed-ssl-certificate-with-mkcert-on-ubuntu-18-04/
Config changes
Config::set('system.environment', 'development');
-->