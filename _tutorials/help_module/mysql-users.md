---
title: MySQL User Creation and Checking
layout: page
type: tute
---

## Using The Terminal To Create a MySQL User And Check Which User Is Logged In

Once you have created your MySQL user you can log in. The following will go over how to check information of the current user.

This is important because when we server request from the browser, it does not use the root user. the browser sends the reqest to the server, the server will run the code with an automatic fake user. This user is only to serve web pages. This means we need to make sure our files have permissions for that user and for that we need to know what that user is called.

First attach a shell to the boilerplate container.

The owner will have the correct permissions for our files. Each file is created with the root user as the owner.<br>
The following command will show you the change owner options.
```bash
chown --help
```
To change the owner and group for all of the files
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

The '*' means 'all' so you are asking to see all the information form the current user. 

The output will give you a table of information about the user. 