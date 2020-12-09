---
title: Creating Item Action
layout: page
type: tute
---

## Creating An Item Action

We now have a button on our index action that directs to 'example-item/edit'. Check the URL to see this. Now we need to create this action and add a form for collecting and saving the item data. <br />
Start by creating a new folder in the actions folder of our module. Call this folder 'item'. This is now a submodule. Submodules are used to isolate actions that relate to a specific object or topic. This way we can easily find and manage all related actions together. <br />
Now create a new file in our 'item' submodule and call it 'edit.php'. In this file add the definition for our action function. This time as we are going to be creating a form, we will need to define two separate functions for our GET and POST methods.
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
Here we need to create the form for adding new item data. For this we will be creating an array of input fields and sending them to multiColForm function from the HTML class.
```php
function edit_GET(Web $w)
{
    //add a title to the action
    $w->ctx('title','Add new item');
    ctxService::getInstance($w)->("title","Add new item");

    // this array is the form definition
    $formData = [
        'Item Data' =>[                         // this is a form section title
            [                                   // each array on this level represents a row on the form. This row has only a single input.
                ['Name','text','name',''],      // this is the input field definition. [Label, type, name, value]
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
    outService::getInstance($w)->(Html::multiColForm($formData, 'example-item/edit'));

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
    $exampleItems = ExampleService::getInstance($w)->getAllItems();

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
To view the table we need to add it to the index action template file.