---
title: Creating Index Template
layout: page
type: tute
---

## Creating The Index Template

Templates are used to define the UI for actions. These files contain both HTML and PHP that get injected into the body of the Cmfive layout, our default action template.

Let's create a template for our example module's index action. Create a folder called 'templates' in our example module. In that folder create a new file called 'index.tpl.php'. Template file names must match the action file name followed by '.tpl.php'.

To add a button to the example index page we are going to use Cmfive's html class. This can be found in 'system/html.php'. We will be using the 'b' function that returns a html button.<br />
Add this code to the 'index.tpl.php'.
```php
<?php

echo Html::b("example-item/edit","Add new item");
```
Now refresh the example index page to view the button. Notice that the URL uses the 'modulename-submodulename/action' format. This indicates that the link is directing to the 'item' submodule of the 'example' module. We now need to add this action to our module. Go to the Creating Item Action section by clicking Next below.

Please note that a button is only one html element which can be added using a template. more can be found in the html.php file in the system folder.
