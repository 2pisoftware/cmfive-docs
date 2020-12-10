---
title: Actions
layout: page
type: tute
---

## Actions

Cmfive actions include pages and asynchronous request endpoints. They are essentially functions that run from URLs. Actions can be either at the module level or separated further through sub modules. <br />
The following example is of an index action located in module_folder -> actions -> index.php.

```php
<?php

function index_ALL(Web $w) {

}
```
The function name before the underscore must match the file name. This is followed by the method, GET, POST or ALL. Finally all actions need to be passed the Web $w object.


## Tutorial

Let's create a few actions for our example module. First we will create an index action that lists all example items stored in the database, then we'll make an 'item' submodule to hold actions for adding, editing and deleting items.

Start by creating a folder called 'actions' in the example module folder. <br />
Create a new file in the actions folder and call it 'index.php' and copy the code below.<br />
```php
<?php

function index_ALL(Web $w) {

    $w->ctx("title", "Example Module");

}
```
The code above we use the 'ctx' or context function on our Web object to set the title for our index action. Our index action is now accessible through the Cmfive UI, click on the 'Example' menu item in Cmfive to view the index action.

The first thing our module needs is a way to add new items to our database. Let's add a button to our index page for adding new items. Buttons and other UI elements are added using module templates. Let's add a template for our index action and create a button, then we will resume adding more actions. For details see [here](templates).

## Tutorial Part 2

We now have a button on our index action that directs to 'example-item/edit', check the URL to see this. Now we need to create this action and add a form for collecting and saving the item data. <br />
Start by creating a new folder in the actions folder of our module, call this folder 'item'. This is now a submodule. Submodules are used to isolate actions that relate to a specific object or topic. This way we can easily find and manage all related actions together. <br />
Now create a new file in our 'item' submodule and call it 'edit.php'. In this file add the definition for our action function. This time as we are going to be creating a form we will need to define two separate functions for our GET and POST methods.
```php
<?php

function edit_GET(Web $w)
{
}

function edit_POST(Web $w)
{
}
```
Let's continue by focussing on the GET method. <br />
Here we need to create the form for adding new item data. For this we will be creating an array of input fields and sending them to multiColForm function from the Html class.
```php
function edit_GET(Web $w)
{
    //add a title to the action
    $w->ctx('title','Add new item');

    // this array is the form definition
    $formData = [
        'Item Data' =>[                         // this is a form section title
            [                                   // each array on this level represents a row on the form. This row has only a single input.
                ['Name','text','name',''],      // this if the input field definition. [Label, type, name, value]
            ],
            [                                   // this row has 3 input fields.
                ['Checked','checkbox','is_checked',0],
                ['Date Started', 'date','dt_started',null],
                ['Number','text','my_integer',0]
            ]
        ]
    ];

    // sending the form to the 'out' function bypasses the template.
    $w->out(Html::multiColForm($formData, 'example-item/edit'));

}
```
Now that we have the form, let's add to the POST function where we will save the data to the database.
```php
function edit_POST(Web $w)
{
    //create a new example item object
    $item = new ExampleItem($w);

    //use the fill function to fill input field data into properties with matching names
    $item->fill($_POST);

    // checkboxes need to be assessed individually as they don't appear in the $_POST array if unchecked
    $item->is_checked = array_key_exists("is_checked", $_POST) ? 1 : 0;

    // function for saving to database
    $item->insertOrUpdate();

    // the msg (message) function redirects with a message box
    $w->msg('Item Saved', '/example');
}
```
Now let's use our service functions to create a list of all saved items on the index action of our module.<br />
Open the index.php action file and add the code to retrieve all items from the database and display them in a table.
```php
function index_ALL(Web $w)
{
    $w->ctx("title","Example Module");

    // access service functions using the Web $w object and the module name
    $exampleItems = $w->Example->getAllItems();

    // build the table array adding the headers and the row data
    $table = [];
    $tableHeaders = ['Name','Checked','Date Started','Number','Actions'];
    if (!empty($exampleItems)) {  // only loop if we have one or more items
        foreach ($exampleItems as $item) { // loop through each item
            $row = [];
            // add values to the row in the same order as the table headers
            $row[] = $item->name;
            $row[] = $item->is_checked ? 'Yes' : 'No';
            $row[] = formatDate($item->dt_started);
            $row[] = $item->my_integer;
            // the actions column is used to hold buttons that link to actions per item. Note the item id is added to the href on these buttons.
            $actions = [];
            $actions[] = Html::b('/example-item/edit/' . $item->id,'Edit Item');
            $actions[] = Html::b('/example-item/delete/' . $item->id, 'Delete', 'Are you sure you want to delete this item?');
            $row[] = implode('',$actions);
            $table[] = $row;
        }
    }

    //send the table to the template using ctx
    $w->ctx('itemTable', Html::table($table,'item_table','tablesorter',$tableHeaders));
}
```
To view the table we need to add it to the index action template file. For details see [here](templates#tutorial-part-2).

## Tutorial Part 3

If we click the 'Edit Item' button on one of our items in the table we go to the item edit action. However this action currently only creates new items. If you look at the URL you will see that the button has appended the item's id number. It's time to modify our edit action so that it looks for an item id in the URL and loads the existing item for editing or if no id is given it creates a new item. <br/>
The following code block shows which lines need to be modified in both the GET and POST edit functions.
```diff
function edit_GET(Web $w) {

+   // we now need to check if we are creating a new item or editing an existing one
+   // we will use pathMatch to retrieve an item id from the url.
+   $p = $w->pathMatch('id');
+   // if the id exists we will retrieve the data for that item otherwise we will create a new item.
+   $item = !empty($p['id']) ? $w->Example->getItemForId($p['id']) : new ExampleItem($w);

    //add a title to the action
+   // change the title to reflect editing or adding a new item
+   $w->ctx('title', !empty($p['id']) ? 'Edit item' : 'Add new item');
-   $w->ctx('title','Add new item');

    // this array is the form definition
    $formData = [
        'Item Data' =>[ // this is a form section title
            [ // each array on this level represents a row on the form. This row has only a single input.
+               // We now need to change the value for each field to reflect the values of the item we are editing.
+               ['Name','text','name',$item->name], // this if the input field definition. [Label, type, name, value]
-               ['Name','text','name',''],      // this if the input field definition. [Label, type, name, value]
            ],
            [ // this row has 3 input fields.
+               ['Checked','checkbox','is_checked',$item->is_checked],
+               ['Date Started', 'date','dt_started',formatDate($item->dt_started)],
+               ['Number','text','my_integer',$item->my_integer]
-               ['Checked','checkbox','is_checked',0],
-               ['Date Started', 'date','dt_started',null],
-               ['Number','text','my_integer',0]
            ]
        ]
    ];

+   // If we are editing an existing item we need to send the id to the post method.
+   if (!empty($p['id'])) {
+       $postUrl = '/example-item/edit/' . $item->id;
+   } else {
+       $postUrl = '/example-item/edit';
+   }
    // sending the form to the 'out' function bypasses the template.
+   $w->out(Html::multiColForm($formData, $postUrl));
-   $w->out(Html::multiColForm($formData, 'example-item/edit'));

}
```
```diff
function edit_POST(Web $w) {

+   // As in the GET method we need to check if we are editing an existing item.
+   $p = $w->pathMatch('id');
+   $item = !empty($p['id']) ? $w->Example->getItemForId($p['id']) : new ExampleItem($w);
-   //create a new example item object
-   $item = new ExampleItem($w);

    //use the fill function to fill input field data into properties with matching names
    $item->fill($_POST);

    // checkboxes need to be assessed individually as they don't appear in the $_POST array if unchecked
    $item->is_checked = array_key_exists("is_checked", $_POST) ? 1 : 0;

    // function for saving to database
    $item->insertOrUpdate();

    // the msg (message) function redirects with a message box
    $w->msg('Item Saved', '/example');
}
```
We can now make changes to our existing items. Test this by changing some of the values of the items in your list.

Our next task will be to create the delete action that will remove items from our list. <br>
Create a new file in actions/item called delete.php and add the following code.
```php
<?php

function delete_ALL(Web $w)
{
    // start by finding the item id included in the URL
    $p = $w->pathMatch('id');
    // check to see if the id has been found
    if (empty($p['id'])) {
        // if no id found use the 'error' function to redirect the use to a safe page and display a message.
        $w->error('No id found for item','example');
    }
    // use the id to retrieve the item
    $item = $w->Example->getItemForId($p['id']);
    // check to see if the item was found
    if (empty($item)) {
        // no item found so let the user know
        $w->error('No item found for id','example');
    }
    // delete the item
    $item->delete();
    // redirect the user back to the item list with a message
    $w->msg('Item deleted','example');
}
```