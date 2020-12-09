---
title: Installation
layout: page
type: tute
---

This guide assumes a working knowledge on how to set up apache to serve a PHP application as well as having an empty MySQL database (with user and password) ready to go.

To install Cmfive, clone or download [the Boilerplate repository](https://github.com/2pisoftware/cmfive-boilerplate) and unpack (if necessary) into a directory of your choosing.

Copy the config.php.example file to config.php and update the database section to contain the credentials of your Cmfive database, e.g.:
```php
Config::set("database", [
    "hostname"  => "localhost",
    "username"  => "cmfive",
    "password"  => "cmfive",
    "database"  => "cmfive",
    "driver"    => "mysql"
]);
```
Change any other configuration items as you see fit then open a terminal in the boilerplate folder and type:
```sh
php cmfive.php
```
Running through commands 1-4 will get you set up and ready to go. Here is an explanation of each command.
1. Will install any third party libraries Cmfive requires via Composer (the composer executable is bundled with the Boilerplate repo)
2. Will install all Cmfive migrations
3. Will set up an administrator user, needed to log in to a new Cmfive install
4. Will generate encryption keys used by Cmfive