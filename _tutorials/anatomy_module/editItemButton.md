---
title: Edit Item Button
layout: page
type: tute
---


## Modifying The Edit Item Button

If we click the 'Edit Item' button on one of our items in the table we go to the item edit action. However, this action currently only creates new items. If you look at the URL you will see that the button has appended the item's id number. It's time to modify our edit action so that it looks for an item id in the URL and loads the existing item for editing or if no id is given it creates a new item. <br/>
The following code block shows which lines need to be modified in both the GET and POST edit functions.
```diff
function edit_GET(Web $w) {

+   // we now need to check if we are creating a new item or editing an existing one
+   // we will use pathMatch to retrieve an item id from the url.
+   $p = $w->pathMatch('id');
+   // if the id exists we will retrieve the data for that item otherwise we will create a new item.
+   $item = !empty($p['id']) ? ExampleService::getInstance($w)->getItemForId($p['id']) : new ExampleItem($w);

    //add a title to the action
+   // change the title to reflect editing or adding a new item
+   $w->ctx('title', !empty($p['id']) ? 'Edit item' : 'Add new item');
-   $w->ctx('title','Add new item');


    // this array is the form definition
    $formData = [
        'Item Data' =>[ // this is a form section title
            [ // each array on this level represents a row on the form. This row has only a single input.
+               // We now need to change the value for each field to reflect the values of the item we are editing.
+               ['Name','text','name',$item->name], // this is the input field definition. [Label, type, name, value]
-               ['Name','text','name',''],      // this is the input field definition. [Label, type, name, value]
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
+   $item = !empty($p['id']) ? ExampleService::getInstance($w)->getItemForId($p['id']) : new ExampleItem($w);
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

function delete_ALL(Web $w) {

    // start by finding the item id included in the URL
    $p = $w->pathMatch('id');
    // check to see if the id has been found
    if (empty($p['id'])) {
        // if no id found use the 'error' function to redirect the user to a safe page and display a message.
        $w->error('No id found for item','example');
    }
    // use the id to retrieve the item
    $item = ExampleService::getInstance($w)->getItemForId($p['id']);
    // check to see if the item was found
    if (empty($item)) {
        // no item found so let the user know
        $w->error('No item found for id','example');
        ctxService::getInstance($w)->error("No item found for id","example");
    }
    // delete the item
    $item->delete();
    // redirect the user back to the item list with a message
    $w->msg('Item deleted','example');
}

```
