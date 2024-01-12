---
title: Cmfive Core
layout: page
type: doc
---

## Hooks

The hook system allows communication between modules within cmfive.
Hooks are based on an event broadcast and listener model.

Within the config.php file of a module exists the ability to register to listen for hook calls from a particular module.

Under the 'hooks' option is a string array of the module names that module is listening to.

```php
<?php

Config::set('task', array(
    'version' => '0.8.0',
    'active' => true,
    'path' => 'system/modules',
    'topmenu' => true,
    "dependencies" => array(
        "floriansemm/official-library-php-email-parser" => "~1.0"
    ),
    'search' => array('Tasks' => "Task"),
    'hooks' => array(
        'core_web',
        'core_dbobject',
        'comment',
        'attachment',
		'timelog',
		'admin',
		'task'
    ),
    'ical' => array(
        'send' => false
    ),
    'timelog' => array(
        'Task'
    ),
    'processors' => array(
        'TicketEmailProcessor'
    )
));
```

This example is from the *task* core module. It is listening for hook broadcasts for the core_web, core_dbobject, comment, attachment, timelog, admin, and task modules. <br/>

To call a hook, use the callHook() method of the Web class.
```php
 /**
     * Call hook method to invoke other modules helper functions
     *
     * @param String module
     * @param String $function
     * @param Mixed $data
     * @return array array of return values from all functions that answer to this hook
     */
    public function callHook($module, $function, $data = null)
```

Calling this method will issue an event to all modules