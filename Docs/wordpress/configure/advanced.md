---
title: Advanced

---

Advanced
========
The *Advanced* panel in the Gantry based template administration interface provides several options for configuring the advanced options for the template. The following configuration options are available:


Maintenance Mode
----------------
*Maintenance Mode* allows you to block the non logged in visitors from viewing your site for the time you're making changes to it. This way you can do modifications and test them without unnecessary rush. By default the front end will display the message specified in the **Message** field, but you can also create your own custom file called `maintenance.php` in the template root directory which will be used instead.

![](assets/advanced-maintenance-mode.jpg)


Display Content
---------------
The *Display Content* option allows you to enable/disable the output of the WordPress content on the front end. This is useful for sites and templates that want to make use of a page that consists entirely of widgets but preserving all Mainbody widget positions.

![](assets/advanced-display-content.jpg)


Mainbody Enabled
----------------
The *Mainbody Enabled* option allows you to enable/disable the entire Mainbody section. This is useful for sites and templates that want to make use of a page that consists entirely of widgets.

![](assets/advanced-mainbody.jpg)


RTL Support
-----------
RTL means “right-to-left” and is a key component when trying to deliver a website in a RTL language such as Hebrew, Arabic, Urdu, etc. Gantry has built in RTL support which will automatically “flip” the content layouts and ordering to support RTL. This option allows you to enable or disable the built-in RTL support which is automatically detected and displayed based on the language file setting.

![](assets/advanced-rtl.jpg)


Disable Auto Paragraphs
-----------------------
The *Disable Auto Paragraphs* option allows you to remove the WordPress filter responsible for automatic `<p>` tag content wrapping. This can be very useful when creating a complex content.

![](assets/advanced-disable-auto-paragraphs.jpg)


Disable Texturize
-----------------
The *Disable Texturize* option disables some text transformations like smart (curly) quotes for content and comments. This can be very useful for example for placing code inside your content.

![](assets/advanced-disable-texturize.jpg)


Template Typography
-------------------
The *Template Typography* option allows you to enable/disable specific typography elements from loading, as well as allowing you to select between light and dark typography.

![](assets/advanced-typography.jpg)


Selectivizr
-----------
Enable or disable *Selectivizr* support for IE8 providing support for additional CSS selectors for better compatibility.

![](assets/advanced-selectivizr.jpg)


LESS Compiler
-------------
*LESS* is commonly used in our Gantry 4 CSS as a server side compiler. Its options allow you to determine the delay on that compiling process, whether CSS compression is also infused within it, and if you wish to debug the header. There is also an option to clear the LESS cache.

![](assets/advanced-less.jpg)

Naming a Custom Override
--------------------------
To rename the custom override, you would need to click on the custom override you want to rename. Then click on the pencil icon as shown in the image below. 
<img src="http://www.rockettheme.com/forum/index.php?id=63160&amp;rb_v=file" alt="7-15-2011 8-03-20 PM.png" onclick="viewableArea(this);">
Then you can hit enter to save the name.
