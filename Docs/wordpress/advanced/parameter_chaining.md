---
title: Parameter Chaining

---

Parameter Chaining
==================
During development of the Gantry Framework, we found that we needed to organize sets of parameters into custom groups of related settings. You can create your own elements in `templateDetails.xml` to allow the setting of specific parameters which you can use later in your own features, layouts, etc. A good example of this is the **pagesuffix** chain that controls any extra CSS classes which should be added to the `<body>` tag. The XML in question looks like this:

~~~ .xml
<fields name="pagesuffix" type="chain" label="PAGESUFFIX" description="PAGESUFFIX_DESC">
	<field name="enabled" type="toggle" default="0" label="ENABLED" enabler="true" />
	<field name="class" type="text" default="" class="text-long" label="CLASS"/>
	<field name="priority" type="hidden" default="2"/>
</fields>
~~~

This parameter block consists of a parent **chain** element. This element has a name called **pagesuffix**. Within the chain, are three elements. One is a toggle called **enabled**, the second a text element named **class**, and third is responsible for the **priority**.

Now, you could get the values of these parameters just by using the call:

~~~ .php
global $gantry;
echo $gantry->get('pagesuffix-enabled');
echo $gantry->get('pagesuffix-menuitem');
~~~

Within Gantry, we have a feature to handle the `pagesuffix` state. This gives us a core gizmo called **GantryGizmoPageSuffix**.

Here's what it looks like:

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

Gizmos, by default, are looking for a chained set of parameters. By setting the `$_feature_name` to **pagesuffix**, and using the feature's own built in `get()` method, we don't need to use the full **pagesuffix-class** chained name. The gizmos method automatically prefixes the feature name to obtain the correct parameter.
