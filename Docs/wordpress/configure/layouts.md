---
title: Layouts

---

Layouts
=======
The Layouts panel in the Gantry-based template administration interface provides several options for configuring the layout of the template. Each widgetized section of the template design offers six widget positions by default.

> [![](../assets/g4-module-widths.jpg)](http://youtube.com/embed/g0iEalGwdJY)
>
> To find out about layouts and widget widths, check out this quick screencast. It covers some of the basic concepts involved in understanding and configuring layouts with a combination of widget configuration and Gantry layout control.


Gantry Divider Widget
---------------------
*Gantry Divider* is a widget used to **tell** Gantry where you want to split your widget position and create another column.

![](assets/layouts-divider-widget.jpg)

If you placed two widgets in one position, they will be displayed in one column in two rows (one above another), but if you're going to place a Gantry Divider Widget between them, they'll be displayed in two columns (one next to each other) with widths set in the Layout settings of that position (for two-widget columns variation). The example below shows the setup where six widgets will be displayed in six columns within a single position.

![](assets/layouts-divider-position.jpg)

The same rule applies to the **MainBody** layout configuration. Splitting your sidebar widgets with one *Gantry Divider* will result in breaking them into a two sidebar layout, exactly in the place where you placed your divider widget. A three-sidebar layout is just a matter of adding a second *Gantry Divider* widget in the **sidebar** widget position.

Using Layouts
-------------
Each of the major widget positions is represented with a slider to allow for dynamic control widget layout. This is based on how many widgets are placed in that position. By default, placed widgets will be displayed at equal sizes.

![](assets/layouts-utility1.jpg)

At the top of the slider are numbered links from 1 to 6 which represent the number of placed widgets you want to configure for. For example, if you are setting up the layout for a position which has four widgets in use (split using three **Gantry Divider** widgets), you will want to first select the #4 link at the top of the slider for that position.

If you had four widgets in one position separated with the **Gantry Divider** widget, your active positions would be 4. The layout slider will always show you the current number of placed widgets in that position. Below that number, a block representation of the current layout is displayed.

We use a system based on [Twitter's Bootstrap](http://twitter.github.com/bootstrap/). Layouts are base 12, and by default, the 12 column `3 | 3 | 3 | 3` of the translates to an equal sized block for all four widgets place in the position.

Based on the 12-column layout with four widgets of equal width published, the front-end will look like this:

![](assets/layouts-utility-example1.jpg)

When you slide the slider bar below to select different widths for these 4 widget columns, a tooltip on the side will also show you the numeric value of the configuration.

![](assets/layouts-utility2.jpg)

In this case, we have positioned the slider to the left and selected the layout `2 | 3 | 4 | 3`, which means that widget column **utility-a** is assigned `2` grids, **utility-b** is assigned `3`, **utility-c** is assigned `4` and **utility-d** is assigned `3` grids. After hitting *Save*, this will cause the front-end's layout to change and display:

![](assets/layouts-utility-example2.jpg)

You can see the `2 | 3 | 4 | 3` proportions have been applied to the layout. Gantry is so flexible that you can configure different layouts for different numbers of placed widgets in a position. Gantry also has the ability to show different widgets on different overrides, so you may have 4 widgets placed on your Home page, but only 2 widgets placed on one of your internal pages, for example. To accommodate this you can merely click the 2 in the **Positions** list and choose a layout that suits your needs:

![](assets/layouts-utility3.jpg)

This will translate into a `8 | 4` or worded another way, a 2/3 and 1/3 distribution of the 2 widgets:

![](assets/layouts-utility-example3.jpg)


Mainbody Layouts
----------------
The layouts for the mainbody area is slightly different from the other widget layouts. The primary difference is that the mainbody is generally displayed along side up to 3 sidebars. This provides the ability for a Gantry-powered template to effectively support a 4 column layout. We researched a wide variety of sites and determined that more than 4 columns for a layout is very rare and quickly becomes unreadable due to the limited amount of space available. Generally speaking 2 or 3 columns is the preferred layout for a modern website.

![](assets/layouts-mb-example1.jpg)

The layout for this is controlled in the template settings. As you can see below, Gantry understands that there are 3 sidebar columns (widgets in sidebars have been splitted using two Gantry Divider widgets), so when the mainbody is taken into account, this creates a 4 column layout. The current configuration is set to `6 | 2 | 2 | 2` where the mainbody is using 6 grid units, and the 3 sidebars each use 2. This adds up to the 12 grid system we are using in this example.

![](assets/layouts-mb1.jpg)

If you drag the slider to the right, you will see the positions shuffle around to display different layout options for the mainbody. With four total columns, there is not much room to have widely varying column widths. So, let's turn off one of the columns by removing one of the *Gantry Divider* widgets in the **sidebar** position using the WordPress widget manager. Below, you will see how the default layout is currently set to display when we have only two sidebars:

![](assets/layouts-mb2.jpg)

As you can see: It's set for the two sidebars to be displayed on the right. Each sidebar is taking up two grid units while the mainbody is on the left occupying eight grid units. Dragging the slider to the right will provide a wide variety of layout options. As you can see below, this example shows a layout of `3 | 6 | 3` with the mainbody in the middle:

![](assets/layouts-mb3.jpg)

After you click the Save button in the toolbar, you will be able to see this layout applied to the frontend:

![](assets/layouts-mb-example2.jpg)
