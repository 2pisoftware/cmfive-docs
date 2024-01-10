---
title: Creating A Config
layout: page
type: tute
---

# Creating A config.php File

```php
<?php

Config::set('MODULE_NAME', [
    'active' => true,
    'path' => 'modules',
    'topmenu' => true,
]);
```

The module config can be used to set a variety of system options as well as any custom module specific options.

The items shown are the minimum required within the config file to achieve a functioning module. You will also need to create a directory caleld modules/ within the example directory you created before.

Cmfive caches config files to aid with page loading times. Changes to config files will require the config cache to be purged and re-written. To purge the config cache click the 'clear configuration cache' button on the cmfive menu.

![Clear configuration cache](/assets/images/config_refresh.png)

In the example module folder, create a file called config.php and insert the following text (this is different to the config.php file changed in the instructions under the installation menu).

```php
<?php

Config::set('example', [
    'active' => true,
    'path' => 'modules',
    'topmenu' => true,
]);
```

Ensure you have created the modules/ directory, if not do this now.

Now clear the config cache and refresh the browser window. You should now see a menu item called 'example'.

![Example menu item](/assets/images/example_menu_item.png)

Now that our module has a config we need to add some tables to the database.

If an error occurs follow the instructions in [The Models Folder](theModelsFolder) and see if this rectifies the issue.
