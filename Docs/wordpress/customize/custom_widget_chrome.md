---
title: Custom Widget Chrome

---

Custom Widget Chrome
====================
This section covers the creation of a Chrome custom widget layout and how to link it into your Gantry enabled template.

Step 1: Planning
----------------
Determine the name of your custom widget position. In this case we will be using "example" as the custom Chrome widget name.

Step 2: Editing html/layouts/chrome_example.php
-----------------------------------------------
The files are located under `YOUR_SITE/wp-content/plugins/gantry/html/layouts/`. However you do not want to modify the core gantry files. Instead copy the new chrome file to `YOUR_SITE/wp-content/themes/YOUR_TEMPLATE/html/layouts`. In this case use `chrome_example.php` Each custom chrome layout requires a `function render()` this is what will be called by Gantry to display the widget. In this case since we have copied an existing chrome this will already be provided.

Example :

~~~ .php
function render($params = array()) {
	global $gantry, $wp_registered_widgets;
	$rparams         = $this->_getParams($params[0]);
	$instance_params = $this->_getWidgetInstanceParams($params[0]['widget_id']);

	$id        = $params[0]['widget_id'];
	$classname = $wp_registered_widgets[$params[0]['widget_id']]['classname'];

	// gantry render params
	$params[0]['pre_widget']   = '';
	$params[0]['widget_open']  = '';
	$params[0]['title_open']   = '';
	$params[0]['title_close']  = '';
	$params[0]['widget_close'] = '';
	$params[0]['post_widget']  = '';
	$params[0]['pre_render']   = '';
	$params[0]['post_render']  = '';

	// normal wp widget params
	$params[0]['before_widget'] = '';
	$params[0]['before_title']  = '';
	$params[0]['after_title']   = '';
	$params[0]['after_widget']  = '';

	if (array_key_exists('custom-variations', $instance_params) && $instance_params['custom-variations'] != '') {
		$params[0]['pre_widget']  = '<div class="' . $instance_params['custom-variations'] . '">';
		$params[0]['post_widget'] = '</div>';
	}

	$params[0]['widget_open']  = sprintf('<div id="%1$s" class="widget %2$s rt-block">', $id, $classname);
	$params[0]['widget_close'] = '</div>';

	$params[0]['title_open']  = '<div class="module-title"><h2 class="title">';
	$params[0]['title_close'] = '</h2></div>';

	if (isset($instance_params['title']) && $instance_params['title'] != '') :
		$params[0]['before_widget'] = $params[0]['pre_widget'] . $params[0]['widget_open'];
		$params[0]['before_title']  = $params[0]['title_open'];
		$params[0]['after_title']   = $params[0]['title_close'] . $params[0]['pre_render'];
		$params[0]['after_widget']  = $params[0]['post_render'] . $params[0]['widget_close'] . $params[0]['post_widget']; else :
		$params[0]['before_widget'] = $params[0]['pre_widget'] . $params[0]['widget_open'] . $params[0]['pre_render'];
		$params[0]['before_title']  = $params[0]['title_open'];
		$params[0]['after_title']   = $params[0]['title_close'];
		$params[0]['after_widget']  = $params[0]['post_render'] . $params[0]['widget_close'] . $params[0]['post_widget'];
	endif;

	return $params;
}
~~~

A full widget chrome looks like the following: 

~~~ .php
class GantryLayoutChrome_Standard extends GantryLayout {
	var $render_params = array(
		'gridCount'   => null,
		'prefixCount' => 0,
		'extraClass'  => ''
	);

	function render($params = array()) {
		global $gantry, $wp_registered_widgets;
		$rparams         = $this->_getParams($params[0]);
		$instance_params = $this->_getWidgetInstanceParams($params[0]['widget_id']);

		$id        = $params[0]['widget_id'];
		$classname = $wp_registered_widgets[$params[0]['widget_id']]['classname'];

		// gantry render params
		$params[0]['pre_widget']   = '';
		$params[0]['widget_open']  = '';
		$params[0]['title_open']   = '';
		$params[0]['title_close']  = '';
		$params[0]['widget_close'] = '';
		$params[0]['post_widget']  = '';
		$params[0]['pre_render']   = '';
		$params[0]['post_render']  = '';

		// normal wp widget params
		$params[0]['before_widget'] = '';
		$params[0]['before_title']  = '';
		$params[0]['after_title']   = '';
		$params[0]['after_widget']  = '';

		if (array_key_exists('custom-variations', $instance_params) && $instance_params['custom-variations'] != '') {
			$params[0]['pre_widget']  = '<div class="' . $instance_params['custom-variations'] . '">';
			$params[0]['post_widget'] = '</div>';
		}

		$params[0]['widget_open']  = sprintf('<div id="%1$s" class="widget %2$s rt-block">', $id, $classname);
		$params[0]['widget_close'] = '</div>';

		$params[0]['title_open']  = '<div class="module-title"><h2 class="title">';
		$params[0]['title_close'] = '</h2></div>';

		if (isset($instance_params['title']) && $instance_params['title'] != '') :
			$params[0]['before_widget'] = $params[0]['pre_widget'] . $params[0]['widget_open'];
			$params[0]['before_title']  = $params[0]['title_open'];
			$params[0]['after_title']   = $params[0]['title_close'] . $params[0]['pre_render'];
			$params[0]['after_widget']  = $params[0]['post_render'] . $params[0]['widget_close'] . $params[0]['post_widget']; else :
			$params[0]['before_widget'] = $params[0]['pre_widget'] . $params[0]['widget_open'] . $params[0]['pre_render'];
			$params[0]['before_title']  = $params[0]['title_open'];
			$params[0]['after_title']   = $params[0]['title_close'];
			$params[0]['after_widget']  = $params[0]['post_render'] . $params[0]['widget_close'] . $params[0]['post_widget'];
		endif;

		return $params;
	}
}
~~~

Upon saving this custom widget chrome will now be available to use in Gantry.


Step 3: Adding Custom Widget Chrome to Gantry
---------------------------------------------
Open up the templates index.php file and find the Gantry widget position you wish to apply your custom widget layout too. In the third function parameter add the name you gave to your Chrome widget after the _ which in the case of the example is "example". See example below: 

~~~ .php
<?php echo $gantry->displayModules('top','standard','example'); ?>
~~~

If you wish to apply this to the main body side bars the layout will look like the following:

~~~ .php
<?php echo $gantry->displayMainbody('mainbody','sidebar', sidebarchromelayout, contenttoplayoutname, contenttopchromename, contentbottomlayoutname, contentbottomchromename); ?>
~~~

Any widget placed in this position will now use this display format.
