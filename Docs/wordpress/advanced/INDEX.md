---
title: Creating New Layout

---

Creating a New Layout
=====================
Layouts are blocks of code that control the HTML structure of a particular section of the template rendering. By default, Gantry comes with several built-in layout files located in the `wp-content/plugins/gantry/html/layouts/` folder:

| Layouts                  | Description
|:-------------------------|:----------------------------------------------------------
| ~~body_iphonemainbody.php~~  | **Deprecated** - Used for iPhone mainbody layout configurations
| body_mainbody.php        | the default mainbody layout. This is the layout that controls the mainbody in relation to the sidebars
| doc_body.php             | a layout to render the body tag, used in `displayBodyTag()`
| doc_tag.php              | a layout used in the generic rendering of a tag output by the `displayClassesByTag()` method
| widget_basic.php         | a basic layout for modules
| widget_sidebar.php       | the layout for the sidebars
| widget_standard.php      | the standard layout for modules
| orderedbody_mainbody.php | renders mainbody and sidebars in order for use with CSS tables


Step 1: Purpose
---------------
The default layout that ships with *Gantry Framework* is designed to be flexible enough to handle the needs of 99% of the possible implementations. However, there are occasions when the default HTML structure does not contain all the blocks elements or class names required to realize a particular design. 

In these rare cases, you can utilize the power of the Gantry framework to override the default layout with your own, template-provided one. Certain instances, such as widget layouts, are flexible enough to support your own custom layouts. You can even call them in the same way the default layouts are called. 


Step 2: Create/Copy New Layout Files
------------------------------------
The simplest way to do this is to copy an existing layout. In this example, we'll copy the **body_mainbody.php** layout and modify it after. The files are located under: 

`[YOUR_SITE]/wp-content/plugins/gantry/html/layouts/`

However, you do not want to modify the core Gantry files. Instead, copy the new layout file to:

`[YOUR_SITE]/wp-content/themes/YOUR_TEMPLATE/html/layouts/`

You may have to create a `layouts/` folder if one does not already exist.

In this case, copy `body_mainbody.php` from the core layouts location into the template layouts location.


Step 3: File Structure
----------------------
After you have copied the `body_mainbody.php` file, you can open it up and edit it to fit your needs. By default, it looks like this:

~~~ .php
<?php
/**
 * @version   $Id: body_mainbody.php 59361 2013-03-13 23:10:27Z btowles $
 * @author    RocketTheme http://www.rockettheme.com
 * @copyright Copyright (C) 2007 - ${copyright_year} RocketTheme, LLC
 * @license   http://www.gnu.org/licenses/gpl-2.0.html GNU/GPLv2 only
 *
 */
defined('GANTRY_VERSION') or die();

gantry_import('core.gantrybodylayout');

/**
 *
 * @package    gantry
 * @subpackage html.layouts
 */
class GantryLayoutBody_MainBody extends GantryBodyLayout
{
    var $render_params = array(
        'schema'            => null,
        'pushPull'          => null,
        'classKey'          => null,
        'sidebars'          => '',
        'contentTop'        => null,
        'contentBottom'     => null,
        'component_content' => ''
    );

    function render($params = array())
    {
        /** @global $gantry Gantry */
        global $gantry;

        $fparams = $this->_getParams($params);

        // logic to determine if the component should be displayed
        $display_mainbody = !($gantry->get("mainbody-enabled", true) == false);
        $display_component = !($gantry->get("component-enabled", true) == false);
        ob_start();
        // XHTML LAYOUT
        ?>
        <?php if ($display_mainbody) : ?>
        <div id="rt-main" class="<?php echo $fparams->classKey; ?>">
            <div class="rt-container">
                <div class="rt-grid-<?php echo $fparams->schema['mb']; ?> <?php echo $fparams->pushPull[0]; ?>">

                    <?php if (isset($fparams->contentTop)) : ?>
                    <div id="rt-content-top">
                        <?php echo $fparams->contentTop; ?>
                    </div>
                    <?php endif; ?>

                    <?php if ($display_component) : ?>
                    <div class="rt-block">
                        <div id="rt-mainbody">
                            <div class="component-content">
                                <?php
                                if ('' == $fparams->component_content) {
                                    $this->include_type();
                                } else {
                                    echo $fparams->component_content;
                                }
                                ?>
                            </div>
                        </div>
                    </div>
                    <?php endif; ?>

                    <?php if (isset($fparams->contentBottom)) : ?>
                    <div id="rt-content-bottom">
                        <?php echo $fparams->contentBottom; ?>
                    </div>
                    <?php endif; ?>

                </div>
                <?php echo $fparams->sidebars; ?>
                <div class="clear"></div>
            </div>
        </div>
        <?php endif; ?>
        <?php
        return ob_get_clean();
    }
}
~~~

Feel free to edit this file as needed.
