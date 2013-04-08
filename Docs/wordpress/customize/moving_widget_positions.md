---
title: Moving Widget Positions

---

Moving Widget Positions
=======================
This section covers moving a widget position within your Gantry enabled template.

> [![](../assets/g4-module-positions.jpg)](http://youtube.com/embed/xYsB2VKmkFU)
>
> Check out this quick screencast on Widget Positions to get an overview of how widget positions work within Joomla and the Gantry Framework.


Step 1: Planning
----------------
Determine which widget position you want to move and where it needs to go within the `index.php` file of the template.


Step 2: Moving Module
---------------------
Copy the Gantry widget position block of code you wish to move. It should look similar to this:

~~~ .html
<?php /** Begin Top **/ if ($gantry->countModules('top')) : ?>
<div id="rt-top" <?php echo $gantry->displayClassesByTag('rt-top'); ?>>
    <div class="rt-container">
        <?php echo $gantry->displayModules('top','standard','standard'); ?>
        <div class="clear"></div>
    </div>
</div>
<?php /** End Top **/ endif; ?>
~~~

Move to area and paste the copied block of code into the new location.
