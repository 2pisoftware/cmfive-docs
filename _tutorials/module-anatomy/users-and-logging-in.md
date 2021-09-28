---
title: Craeting More Users and Logging in
layout: page
type: tute
---
Login and password is what you should use for creating new tables. This can be found on the page /system/modules/auth/models/User.php.


Most of the information required will be automated to simplify creating users. This means people creating users for your module will not be hit with all the possible roles for the crm when trying to create a new user.<br> Remember, this will be an alternative way to add a new user instead of going through Admin add user.

The form definition can be found in the form template in /system/admin/templates/useradd.tpl.php.

From the file /system/admin/models/useradd.php, we can see that when a new user is created, it will check that the passwords match. If they do not, they will throw an error. 

![Password Match Error](/assets/images/password_match.png)

You will need to add this code to your own add user function for your module. It will go in the POST function of your edit action for your user (/example/actions/useredit.php).<br>
If it throws an error your file should set it to return to a list of users.

The $contact->fill and $contact->insertOrUpdate should be below this.