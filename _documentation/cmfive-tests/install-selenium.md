---
title: Cmfive Test Framework
layout: page
type: doc
---

## Set up Selenium

This guide assumes Codeception and additional PHP libraries are already installed, see: [Installation](/documentation/cmfive_tests/install-codecept).

Cmfive tests use the Codeception WebDriver module. WebDriver applies test actions through simulated or actual browser sessions and Selenium offers ideal support. Currently Cmfive tests expect Selenium version 3.14.0 for compatibility with the FaceBook PHP WebDriver API used internally by Codeception.

Browser interfaces are provided by vendors in additional WebDriver executables. Selenium itself is a Java package. A Java run time environment must be available. There are many ways to set up Selenium.

If you use Docker, a 'headless' SeleniumStandalone image is an effective approach.
eg:
```batch
docker run --net=host selenium/standalone-chrome:3.14.0
```

If you rather start from scratch on your local machine, first download and unpack Selenium into any preferred folder. Into the same folder, download and unpack a Selenium WebDriver for your intended browser: ChromeDriver, for Chrome, or GeckoDriver for Firefox.

Then, launch the Selenium jar:
```batch
java -jar ./selenium-server-standalone-3.14.0.jar
```
Selenium will find the WebDrivers in the folder it is launched from. This simplifies needing runtime settings.

When Selenium launches, you should see a log like:
```log
cmfive-boilerplate\test\Services\Windows>java -jar .\selenium-server-standalone-3.14.0.jar
11:49:32.317 INFO [GridLauncherV3.launch] - Selenium build info: version: '3.14.0', revision: 'aacccce0'
11:49:32.330 INFO [GridLauncherV3$1.launch] - Launching a standalone Selenium Server on port 4444
2020-03-03 11:49:32.835:INFO::main: Logging initialized @1406ms to org.seleniumhq.jetty9.util.log.StdErrLog
11:49:33.891 INFO [SeleniumServer.boot] - Selenium Server is up and running on port 4444
```

Make note of the port Selenium is listening on. Port 4444 is most usual.

By example, for Windows, see the folder:
```batch
cmfive-boilerplate\test\Services\Windows
```
This is ready to go by running:
```batch
LaunchChromeSelenium.bat
```