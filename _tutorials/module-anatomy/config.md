---
title: Config
layout: page
type: tute
---

# config.php

```php
<?php
Config::set('MODULE_NAME', [
    'active' => true,
    'path' => 'modules',
    'topmenu' => true,
]);
```

The module config can be used to set a variety of system options as well as any custom module specific options.

The items shown are the minimum required to achieve a functioning module.

Cmfive caches config files to aid with page loading times. Changes to config files will require the config cache to be purged and re-written. To purge the config cache click the 'clear configuration cache' button on the cmfive menu.

![Clear configuration cache](/assets/images/config_refresh.png)

# Tutorial

In the example module folder, create a file called config.php and insert the following text.

```php
<?php
Config::set('example', [
    'active' => true,
    'path' => 'modules',
    'topmenu' => true,
]);
```

Now clear the config cache and refresh the browser window. You should now see a menu item called 'example'.

![Example menu item](/assets/images/example_menu_item.png)

Now that our module has a config we need to add some tables to the database. For details see [here](install).