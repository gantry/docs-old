---
title: Template Overrides

---

Template Overrides
==================
Gantry offers the ability to override default template configurations for individual menu items. A frequent example is to have different layout configurations for your site's frontpage, versus subpages. Gantry makes this achievable in just a few clicks.

> [![](../assets/g4-overrides.jpg)](#)
>
> Discover the power of Gantry and it's ability to configure any parameter based on template overrides using custom template styles. Gantry adds the power of inheritance of settings to enable easier per-menu custom configurations.


Creating an Override
--------------------
There are two methods of creating a new set of assignable configurations. The first is the **Save as Copy** method, which involves you editing the Gantry template Master at **Extensions → Template Manager → gantry — Default (Master)**. Configure your settings, change the **Style Name** and select **Save as Copy** from the **Save** dropdown.

![](assets/template-override-save-as-copy.jpg)

Alternatively, from the **Template Manager**, you can select the checkbox for the Gantry template Master, and click **Duplicate** from the button toolbar. It will automatically create a copy, and mark it as **Override**.


Configuring an Override
-----------------------
Once an **Override** has been created, you simply need to open it and configure. Each tab will have greyed out parameters that can be activated via the checkbox.

![](assets/template-override-assigned-params.jpg)

Configure items, then click on the **Assignments** tab. All menu items are listed here, so just check the items you wish this particular Override to apply to.

![](assets/template-override-assign-menus.jpg)


Override Examples
-----------------
Below is a simple example of an Override. The **Layouts → MainBody Positions** setting has been overridden for a menu item. Therefore, in the screenshots below, you can see that the sidebar allocation can be either left or right of the mainbody, and not be applied globally. This is the same for other settings as well, such as Features or Styles.

| ![][example1] | ![][example2] |
|---------------|---------------|
| ![][config1]  | ![][config2]  |


[config1]: assets/template-override-example-config1.jpg
[config2]: assets/template-override-example-config2.jpg
[example1]: assets/template-override-example1.jpg
[example2]: assets/template-override-example2.jpg
