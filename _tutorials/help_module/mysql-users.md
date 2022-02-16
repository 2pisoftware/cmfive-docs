---
title: MySQL User Creation and Checking
layout: page
type: tute
---

## Using The Terminal To Create a MySQL User

<!--Creating MySQL user-->
<!-- Use config_hostname photo-->
Connect a shell to the mysql container (labelled mysql:5.7.21 or similar).

Type the following command into the terminal:
```sh
mysql -uroot -p
```

It will ask you for a password. This is just 'root'.

You are now logged in as the root user who has full access to all the databases. However, we never do our coding using the root MySQL user as it is insecure. It is unlikely, but even if you want full access to all of the databases, it is best practice to create another user who also has these permissions. 

Type the following in to the terminal to create your new user.

```bash
CREATE USER 'cmfive'@'mysql-5.7' IDENTIFIED BY 'cmfive';
```

The first part in inverted commas ('') is the name of our user. The second part is the hostname. mysql-5.7 is the host we set for the cmfive database under the [installation instructions](/tutorials/installation/installation). The last word in inverted commas is the password for our new user.<br>
Our new user, cmfive, will need access to the cmfive database. Type the below command into the terminal to grant this.

```bash
GRANT ALL PRIVILEGES ON cmfive . * TO 'cmfive'@'mysql-5.7';
```

The first cmfive in the above command refers to the cmfive database. The '*" is in the table position of the command. '*' means all in the terminal, so the above command is granting the user access and all privileges on all the tables in the cmfive database.

Whenever you make changes to the database permissions you need to flush privileges

```bash
FLUSH PRIVILEGES;
```

Your changes will now be in effect.