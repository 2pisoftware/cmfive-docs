---
title: cmfive-core set up
layout: page
type: tute
---

## Set up cmfive-core For Development

To start you will need to clone the cmfive-boilerplate. Go to the 2pi Software account on GitHub, and navigate to the cmfive-boilerplate. Above the repository file on the left, click the green button labelled 'Code'. Copy the link in the popup.

Now open your Git application, and choose to clone a repository from GitHub. Make sure it will save on your device in the folder that your web server points to. Use the copied URL in the relevant box and hit clone.

When you clone the boilerplate, cmfive-core can be installed by following the instructions under [Installation](/tutorials/installation). The next step is to set this up separately in your Git application.

Open your Git application choose to open a repository. Find where you cloned the boilerplate to. Go to the following path **composer/vendor/2pisoftware/cmfive-core** composer folder in boilerplate.

![path to cmfive-core](/assets/images/cmfive-core_path.png)

Now you'll be able to use the cmfive-core in your Git application.

<b>Please Note:</b> For live/production deployment it is expected cmfive will refuse TLS1.0&1.1 connections, for improved security.
This may not be the case, with default setup of your web server.
But be aware, making a change may affect very old browsers ability to connect to cmfive.

For a Linux system with Apache:

To find SSL configuration references, run:
grep -i -r "SSLEngine" /etc/apache2

eg:
/etc/apache2/sites-available/default-ssl.conf:          SSLEngine on
/etc/apache2/sites-available/default-ssl.conf:                SSLEngine on
/etc/apache2/sites-available/000-default.conf:  SSLEngine on

Add these entries to the files:
```php
SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder on
SSLCipherSuite "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS !RC4"
```