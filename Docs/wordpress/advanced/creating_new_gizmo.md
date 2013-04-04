---
title: Creating a New Gizmo

---

Creating a New Gizmo
======================
In the Gantry framework we use the term Gizmo to refer to a specific bit of functionality. Gizmos are flexible enough that they can be used to perform almost any kind of logic you would need. The base GantryGizmo class contains methods that can be implemented to control how your gizmo functions. Those methods are:

| `isEnabled()`
|:-------------------------------------------------------------------------------------------------------------------------------------------------------
| by default this gets its state from the enabled toggle in the admin. You can override this to force the enabling of a gizmo without any UI interaction.
| Returns `boolean` [true | false]


| `setPrefix(string $prefix)`
|:------------------------------------------------------------------------
| sets a prefix for handling prefixed parameters such as chained elements.
| Argument `string` [prefix name - usually the name of the main chain param]


| `get($param [, $prefixed = true])`
|:-----------------------------------------------------------------------------------------
| gets a param from the gizmo's configuration. Can also take a prefix for more specificity.
| Argument `string` [field name]
| Argument [optional] `boolean` [true | false]
| Returns `mixed` [the current value of the field]


| `init()`
|:-----------------------------------------------------------------------------------------------------------
| by default empty. Is the first method called on initialization of a gizmo. Used for setup or initialization


| `query_parsed_init()`
|:-----------------------------------------------------------------
| by default empty. Initializes the gizmos after query gets parsed.


| `admin_init()`
|:-------------------------------------------------------------------------------------
| by default empty. Used to initialize gizmo when the admin dashboard gets initialized.


| `finalize()`
|:--------------------------------------------------
| by default empty. Called at the end of the gizmo

All core gizmos and any custom gizmo you create, should extend this GantryGizmo class. To create a new gizmo of your own, you would just have to create a new file in your gizmos/ folder that extended the GantryGizmo class. It will automatically get picked up by the Gantry framework and be processed. The best way to see what a gizmo can do for you is to examine a few of the core gizmos.


ToTop Feature
-------------
First let's look at one of the core features called `totop.php`. As you can imagine the **totop** feature is intended to display a link at the bottom of your page and provide a smooth-scroll back to the top of the page. The most important part of a feature is the actual feature PHP file. The core features are located in the `libraries/gantry/features/` folder. These should **never** be touched or changed.

If you want to override the behavior of a core feature, simply copy the core feature in your `/templates/[YOUR_TEMPLATE]/features` folder. Gantry will automatically pick up your version of the file and use it rather than the default version if you have created one with the same name. The other part of a feature and one that is totally optional is the configuration section. As with other parts of Gantry, the configuration is handled in the `template-options.xml`.

For the **totop** feature the section in the `template-options.xml` looks like:

~~~ .xml
<fields name="totop" type="chain" label="TOTOP" description="TOTOP_DESC">
    <field name="enabled" type="toggle" default="0" label="SHOW"/>
    <field name="position" type="position" default="copyright-b" label="POSITION"/>
    <field name="text" type="text" default="Back to Top" label="TEXT" class="text-long" />
</fields>
~~~

What this means is that in the administrator interface, there are going to be three fields rendered. One is a toggle element that will control the 'enabled' state and the second is position element that controls the position the feature is rendered in. The third field is a text field that allows you to enter some custom text. By exposing these elements in the XML, we allow interaction with the user. If you wanted to add new elements in this XML section, you could, and they would be available for you to use in your feature's PHP definition.

Next, let's look at the PHP for this feature:

~~~ .php
<?php
/**
 * @version   $Id: totop.php 2487 2012-08-17 22:04:06Z btowles $
 * @author    RocketTheme http://www.rockettheme.com
 * @copyright Copyright (C) 2007 - ${copyright_year} RocketTheme, LLC
 * @license   http://www.gnu.org/licenses/gpl-2.0.html GNU/GPLv2 only
 *
 * Gantry uses the Joomla Framework (http://www.joomla.org), a GNU/GPLv2 content management system
 *
 */

defined('JPATH_BASE') or die();

gantry_import('core.gantryfeature');

/**
 * @package     gantry
 * @subpackage  features
 */
class GantryFeatureToTop extends GantryFeature
{
    var $_feature_name = 'totop';

    function init()
    {
        /** @var $gantry Gantry */
        global $gantry;

        if ($this->get('enabled')) {
            $gantry->addScript('gantry-totop.js');
        }
    }

    function render($position)
    {
        ob_start();
        ?>
    <div class="clear"></div>
    <div class="rt-block">
        <a href="#" id="gantry-totop" rel="nofollow"><?php echo $this->get('text'); ?></a>
    </div>
    <?php
        return ob_get_clean();
    }
}
~~~

As you can see the there are two methods implemented in the PHP definition of the feature. The first overrides the default `init()` method and this is used to setup the feature. In this case we are simply using it to added some JavaScript that will provide the smooth scrolling. The second method that is used is `render()`.

This method actually renders out the link and the custom text field that was defined in the administrator interface. The other methods from the base GantryFeature class are not overridden. That means that the standard methods to get the enabled state, position, etc are being used and are pulling that data from the XML and the admin settings. You can see how custom XML fields like **text** are easily available and are prefixed by the feature name, so you can just use `get->("text")` to retrieve the value of of the chained field.

Have a look through all the [default features](../configure/features.md) that come with Gantry to see how we achieved a wide variety of functionality with these features.
