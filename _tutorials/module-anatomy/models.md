---
title: Models
layout: page
type: tute
---

# Models

Models is where we store of class definitions. These usually relate to our database tables but also includes a module service class for holding module level functions.

# Tutorial

Let's create our models folder, our example service class and a model for our example item.

In our example module, create a folder called 'models'.

Now let's make our service class for our module. <br />
In the models folder create a new file called 'ExampleService.php'. All files in the models folder need to be named using camel case and have the module name prepended.<br />
Open the file and add the class definition.
```php
<?php

class ExampleService extends DbService
{
}
```
Let's add two functions to our service class that will be used to retrieve data for our example items. These functions will use GetObject functions from Cmfive's DbService class. Add these functions to the service class.
```php
// returns all example item instances
public function GetAllItems()
{
    return $this->GetObjects('ExampleItem',['is_deleted'=>0]);
}

// returns a single example item matching the given id
public function GetItemForId($id)
{
    return $this->GetObject('ExampleItem',$id);
}
```

Now let's create our class for the example item object. <br />
Create a new file in the models folder called 'ExampleItem.php'. Model file names need to reflect the database table name only in camel case, previously we created a table called 'example_item' now have created the corresponding model called 'ExampleItem'. <br />
Let's start defining our model properties in our 'ExampleItem.php' file.
```php
<?php

class ExampleItem extends DbObject
{
    public $name;
    public $is_checked;
    public $dt_started;
    public $my_integer;
}
```
The model properties must be named according to the column names on the database table.

Now that we have our model and service class we can start creating some actions for our module. For details see [here](actions).