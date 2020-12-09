---
title: Using The Log
layout: page
type: tute
---

## Fixing Errors Using the Logs

If you get an error message at any point when you display your code in localhost, Cmfive will diagnose it for you using the logs.

Finding the logs is simple. First, open the boilerplate. Go to the .build folder, the storage folder, and the logs folder. The files here store information about every time the Cmfive database has been accessed.

Note that each of the log names have cmfive, followed by a date, and are appended by '.log'. To find the log for your error, select the log that has todays date in the name (this should be at the bottom of the list). All entries in the log files start with a date and time stamp in square brackets. Scroll down to the last entry of your file.

For an error the file will show 'cmfive.ERROR' after the date and time stamp. This will be followed by a brief description of the error and 'trace:' which will give the path to the code with the error, followed by the line it's in. For example, the path to the logs is written as cmfive-boilerplate/storage/log.

By following this path, and checking the line shown in the brackets after the path, you should be able to locate the error in your code.

Sometimes you will want to test the logs by adding a test error, info, debug, or warn (warning) to the log. You can do this in your index.php file in the actions folder cmfive-boilerplate/modules/example/actions/index.php.

Remember to set your Example Module using setLogger.

Copy the line from the code below into your index.php file.

```php
<?php

function index_ALL(Web $w) {
    $w-ctx("title", "Example Module");

    // Service classes should be invoked using MyService::getInstance($w), e.g.
    LogService::getInstance($w)->setLogger("EXAMPLE")->error("This is a test");
    LogService::getInstance($w)->setLogger("EXAMPLE")->info("This is a test");
    LogService::getInstance($w)->setLogger("EXAMPLE")->debug("This is a test");
    LogService::getInstance($w)->setLogger("EXAMPLE")->warn("This is a test");
}
```

Note: You will encounter "old" ways of referencing service classes like $w->Log->error(), e.g

```php
$w->Log->error("This is an error message")
```

If you check your most recent log, you should see an error, info, debug, and warning described as 'This is a test'.

![Log error test result](/assets/images/log_example.png)

Remember, the most recent log will be the last one in the folder, and your error should be the last line in the file.