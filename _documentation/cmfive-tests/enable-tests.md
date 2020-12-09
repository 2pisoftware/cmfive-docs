---
title: Cmfive Test Framework
layout: page
type: doc
---

## Enable the Test Runner

This guide assumes Codeception is installed and Selenium configured with WebDriver in place, see: [Installation](/documentation/cmfive_tests/config-web-driver).

The test framework is powerful and should not be enabled in live or production environments - it will allow unaware users to destroy data if running tests inappropriately! Make use of Cmfive scripts to manage and protect your database.

Enabling the test framework is simple. Edit the file:
```batch
cmfive-boilerplate/config.php
```
Update the 'testrunner' setting to 'ENABLED'.
```php
//========== TestRunner Configuration ==========================
//========== must be "ENABLED" to run ==========================
//========== "config" will pass through to CmfiveSite helper ===
Config::append("tests", array(
	"testrunner"  =>  "ENABLED" ,
		'config' => [ ]
));
```
The Cmfive test libraries do not need any extra entries to be added in the TestRunner 'config' array setting.

Make sure you refresh the Cmfive configuration cache, then run:
```batch
php cmfive-boilerplate/cmfive.php
```

You should see new menu items added to manage tests.