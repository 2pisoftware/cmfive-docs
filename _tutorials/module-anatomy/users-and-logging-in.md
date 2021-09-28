---
title: Craeting More Users and Logging in
layout: page
type: tute
---
Login and password is what you should use for creating new tables. This can be found on the page /system/modules/auth/models/User.php.


Most of the information required will be automated to simplify creating users. This means people creating users for your module will not be hit with all the possible roles for the crm when trying to create a new user.<br> Remember, this will be an alternative way to add a new user instead of going through Admin add user.

The form definition can be found in the form template in /system/admin/templates/useradd.tpl.php.