---
title: Parameter Chaining

---

Parameter Chaining
==================
During the development of the Gantry Framework, we found we needed to organize sets of parameters into custom groups of related settings. You can create your own elements in the templateDetails.xml to allow the setting of specific parameters that you can use later in your own features, layouts, etc. A good example of this is the **pagesuffix** chain that controls if any extra CSS classes should be added to the `<body>` tag. The XML in question looks like this:

~~~ .xml
<fields name="pagesuffix" type="chain" label="PAGESUFFIX" description="PAGESUFFIX_DESC">
	<field name="enabled" type="toggle" default="0" label="ENABLED" enabler="true" />
	<field name="class" type="text" default="" class="text-long" label="CLASS"/>
	<field name="priority" type="hidden" default="2"/>
</fields>
~~~

This parameter block consists of a parent **chain** element. This element has a name called **pagesuffix**. Within the chain, are three elements, one is a toggle called **enabled**, second is a text element named **class** and third responsible for the **priority**.

Now, you could get the values of these parameters just by using the call:

~~~ .php
global $gantry;
echo $gantry->get('pagesuffix-enabled');
echo $gantry->get('pagesuffix-menuitem');
~~~

However, within Gantry we have a feature to handle the 'pagesuffix' state, and therefore we have a core gizmo called GantryGizmoPageSuffix that looks like:

~~~ .php
class GantryGizmoPageSuffix extends GantryGizmo {
	var $_name = 'pagesuffix';

	function query_parsed_init()
	{

		/** @global $gantry Gantry */
		global $gantry;

		//add body class suffix
		$gantry->addBodyClass($gantry->get('pagesuffix-class'));

	}

}
~~~

Gizmos by default are looking for a chained set of parameters, so by setting the `$_feature_name` to **pagesuffix**, and using the feature's own built in `get()` method, we don't need to use the full **pagesuffix-class** chained name, as the gizmos method automatically prefixes the feature name to obtain the correct parameter.
