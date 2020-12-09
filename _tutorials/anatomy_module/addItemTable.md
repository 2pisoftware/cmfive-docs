---
title: Add Item Table
layout: page
type: tute
---


## Adding The Item Table to The Index Template

Adding the item table to the index template.

Open templates/index.tpl.php and add the following lines.
```php
<?php echo Html::b("example-item/edit","Add new item"); ?>
<?php echo $itemTable; ?>
```
The item table is now visible on the index action. Use the add new item button to add a few more items to the table.<br />
Now we need to get our item action buttons to work properly. We will do this in the Edit Item Button section.