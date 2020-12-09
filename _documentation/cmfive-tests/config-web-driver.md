---
title: Cmfive Test Framework
layout: page
type: doc
---

## Configure WebDriver

This guide assumes Codeception is installed with Selenium provisioned, see: [Installation](/documentation/cmfive_tests/install-selenium).

Cmfive tests use the Codeception WebDriver module and Selenium to apply test actions. WebDriver support is provided by browser vendors in additional executables. Make sure Selenium can find the WebDriver for your intended browser: ChromeDriver, for Chrome, or GeckoDriver for Firefox.

When you launch Selenium you should see a log like:
```log
cmfive-boilerplate\test\Services\Windows>java -jar .\selenium-server-standalone-3.14.0.jar
11:49:32.317 INFO [GridLauncherV3.launch] - Selenium build info: version: '3.14.0', revision: 'aacccce0'
11:49:32.330 INFO [GridLauncherV3$1.launch] - Launching a standalone Selenium Server on port 4444
2020-03-03 11:49:32.835:INFO::main: Logging initialized @1406ms to org.seleniumhq.jetty9.util.log.StdErrLog
11:49:33.891 INFO [SeleniumServer.boot] - Selenium Server is up and running on port 4444
```
Make note of the port Selenium is listening on. Port 4444 is most usual.

Now, create or edit the file:
```batch
cmfive-boilerplate/test/Codeception/tests/acceptance.suite.dist.yml
```
Set 'port' to the port Selenium listens on, 'browser' to your WebDriver type and 'url' to your Cmfive hosting.
For example:
```yml
	modules:
	  enabled:
		- WebDriver:
			url: http://cmfive.local
			browser: chrome
			wait: 60
			port: 4444
```

If the file is not present, duplicate a fresh one for use from the versioned example:
```batch
acceptance.suite.dist.yml.example
```