---
title: Parameter Chaining

---

Parameter Chaining
==================
During the development of the Gantry Framework, we found we needed to organize sets of parameters into custom groups of related settings. You can create your own elements in the templateDetails.xml to allow the setting of specific parameters that you can use later in your own features, layouts, etc. A good example of this is the **inactive** chain that controls what menu item should be displayed when the menu is inactive. The XML in question looks like this:

~~~ .xml
<param name="inactive" type="chain" label="INACTIVE"  description="INACTIVE_DESC">
    <param name="enabled" type="toggle" default="1" label="ENABLED"  setinmenuitem="false" />
    <param name="menuitem" type="menuitem" label="SELECT_MENU_ITEM" setinmenuitem="false" />
</param>
~~~

This parameter block consists of a parent **chain** element. This element has a name called **inactive**. Within the chain, are two elements, one is a toggle called **enabled** and the other is a menuitem element named **menuitem**.

Now, you could get the values of these parameters just by using the call:

~~~ .php
global $gantry;
echo $gantry->get('inactive-enabled');
echo $gantry->get('inactive-menuitem');
~~~

However, within Gantry we have a feature to handle the 'inactive' state, and therefore we have a core feature called GantryFeatureInactive that looks like:

~~~ .php
class GantryFeatureInactive extends GantryFeature {
    var $_feature_name = 'inactive';

    function init() {
        global $gantry, $Itemid;

        $enabled = $this->get('enabled');
        if($enabled) {
            $menus = &JSite::getMenu();
            $menu  = $menus->getActive();
            if (null == $menu){
                $menuitem = $this->get('menuitem');
                $menus->setActive($menuitem);
                $Itemid = $menuitem;
            }
        }
    }
}
~~~

Features by default are looking for a chained set of parameters, so by setting the `$_feature_name` to **inactive**, and using the feature's own built in `get()` method, we don't need to use the full **inactive-menuitem** chained name, as the feature's method automatically prefixes the feature name to obtain the correct parameter.
