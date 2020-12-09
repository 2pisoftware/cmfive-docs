---
title: Templates
layout: page
type: tute
---

## Templates

Templates are used to define the UI for actions. These files contain both HTML and PHP that get injected into the body of the Cmfive layout, our default action template.

## Tutorial

Let's create a template for our example module's index action. Create a folder called 'templates' in our example module. In that folder create a new file called 'index.tpl.php'. Template file names must match the action filename followed by '.tpl.php'.

To add a button to the example index page we are going to use Cmfive's html class. This can be found in 'system/html.php'. We will be using the 'b' function that returns a html button.<br />
Add this code to the 'index.tpl.php'.
```html
<?php echo Html::b("example-item/edit","Add new item"); ?>
```
Now refresh the example index page to view the button. Notice that the URL uses the 'modulename-submodulename/action' format. This indicates that the link is directing to the 'item' submodule of the 'example' module. We now need to add this action to our module. Resume the actions tutorial [here](actions#tutorial-part-2)

## Tutorial Part 2

Adding the item table to the index template.

Open templates/index.tpl.php and add the following lines.
```php
<?php echo Html::b("example-item/edit","Add new item"); ?>
<?php echo $itemTable; ?>
```
The item table is now visible on the index action. Use the add new item button to add a few more items to the table.<br />
Now we need to get our item action buttons to work properly. We will do this back in the actions section. Resume the actions tutorial [here](actions#tutorial-part-3)
