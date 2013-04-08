---
title: Adding Widget Positions

---

Adding Widget Positions
=======================
This section covers how to add a new widget position to the Gantry Framework and to your Gantry enabled template.

> [![](../assets/g4-module-positions.jpg)](http://youtube.com/embed/xYsB2VKmkFU)
>
> Check out this quick screencast on Widget Positions to get an overview of how widget positions work within WordPress and the Gantry Framework.


Step 1: Getting Ready
---------------------
Determine the position name and location on your theme where you would like your new position to appear. In our example we will use "example".


Step 2: Adding Position to index.php
------------------------------------
Open your template `index.php` file and go to where you would like to add your new position. Using `$gantry` we will make a call to the object using the function `displayModules(positionname, widgetlayouttype, widgetchromelayout);` This call will need to be echoed.

Example:

~~~ .html
<div id="rt-exampleposition">
  <?php echo $gantry->displayModules('example','standard','standard'); ?>
  <div class="clear"></div>
</div>
~~~

The position now will appear after we have configured the Gantry portion to recognize it. Until then it will not work properly.


Step 3: Adding Position to Gantry Framework
-------------------------------------------
Open `templateDetails.xml` and scroll down to the "positions" tag where the default Gantry positions are listed. Under here we will need to add our "row module" positions a through f as in the example below:

~~~ .xml
<position id="example" name="Example" max_positions="6">Example</position>
~~~

Next scroll down to the line which says:

~~~ .xml
<fieldset name="layouts" label="LAYOUTS">
~~~

This is where we add our new position layout slider. We need to add the following xml block to make this appear in the Template Settings :

~~~ .xml
<fields name="example" type="position" label="Example" description="LAYOUT_POS_DESC">
    <field name="layout" type="positions" default="3,3,3,3" label="">
        <schemas>1,2,3,4,5,6</schemas>
        <words>2,3,4,5,6,7,8,9,10</words>
    </field>
    <field name="showall" type="toggle" default="0" label="FORCE_POS"/>
    <field name="showmax" type="showmax" default="6" label="POS_COUNT"/>
</fields>
~~~

| Attribute    | Description                                                                       |
|:-------------|:----------------------------------------------------------------------------------|
|        name  | name of position                                                                  |
|        type  | must always be "position"                                                         |
|     default  | default layout for the widget position any combination of 12 separated by commas. |
|       label  | Label in Template Settings for this position.                                     |
| description  | description of what this area is used for.                                        |


