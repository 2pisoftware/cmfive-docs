---
title: Creating Index Action
layout: page
type: tute
---

## Creating The Index Action

Cmfive actions include pages and asynchronous request endpoints. They are essentially functions that run from URLs. Actions can be either at the module level or separated further through sub modules. <br />
The following example is of an index action located in module_folder -> actions -> index.php.

```php
<?php

function index_ALL(Web $w)
{
}
```
The function name before the underscore must match the file name. This is followed by the method, GET, POST or ALL. Finally, all actions need to be passed the Web $w object.

Let's create a few actions for our example module. First we will create an index action that lists all example items stored in the database, then we'll make an 'item' submodule to hold actions for adding, editing and deleting items.

Start by creating a folder called 'actions' in the example module folder. <br />
Create a new file in the actions folder and call it 'index.php' and copy the code below.<br />
```php
<?php

function index_ALL(Web $w)
{
    $w->ctx("title", "Example Module");
}
```
In the code above we use the 'ctx' or context function on our Web object to set the title for our index action. Our index action is now accessible through the Cmfive UI. Click on the 'Example' menu item in Cmfive to view the index action.

The first thing our module needs is a way to add new items to our database. Let's add a button to our index page for adding new items. Buttons and other UI elements are added using module templates. Let's add a template for our index action and create a button. Then we will add more actions.