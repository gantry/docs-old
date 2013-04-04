---
title: Custom Widget Layout

---

Custom Widget Layout
====================
In this section we will go over creating a custom XHTML layout for widgets in a Gantry enabled template.


Step 1: Preparation
-------------------
Determine the name of your custom widget layout.


Step 2: Create/Copy New Layout File
-----------------------------------
The simplest way to do this is to copy an existing layout and modifying them after. The files are located under `YOUR_SITE/wp-content/plugins/gantry/html/layouts/`. However you do not want to modify the core gantry files. Instead copy the new layout file to `YOUR_SITE/wp-content/themes/YOUR_TEMPLATE/html/layouts`. In this case use `widget_standard.php`


Step 3: File Structure
----------------------
Each custom widget layout requires a function render() this is what will be called by gantry to display the layout. In this case since we have copied an existing layout this will already be provided.

At the top of this widget layout there are gantry specific items which should not be modified. These are:

~~~ .php
function render($params = array()) {
	/** @global $gantry Gantry */
	global $gantry;
	$instance_params = $this->_getWidgetInstanceParams($params[0]['widget_id']);
	$chrome_to_use   = (isset($instance_params['widget_chrome']) && !empty($instance_params['widget_chrome'])) ? $instance_params['widget_chrome'] : $params[0]['chrome'];
	$params          = $gantry->renderLayout("chrome_" .$chrome_to_use, $params);

	$params[0]['position_open']  = '';
	$params[0]['position_close'] = '';

	$rparams   = $this->_getParams($params[0]);
	$start_tag = "";

	// see if this is the first widget in the postion
	if (property_exists($rparams, 'start') && $rparams->start == $rparams->widget_id) {
		$prefixClass = '';
		// get the prefix class for the start
		if ($rparams->widget_map[$rparams->position]['prefixCount'] != 0) {
			$prefixClass = " rt-prefix-" . $rparams->widget_map[$rparams->position]['prefixCount'];
		}
		ob_start();
		// XHTML LAYOUT
		.....
~~~

After the `ob_start();` is where the layout should be written in XHTML.

After adding your XHTML code block there must be a return with a call to `ob_get_clean();` This is required for this function.

~~~ .php
		$start_tag = ob_get_clean();
		$params[0]['position_open'] = $start_tag;
	}

	if (property_exists($rparams,'end') && $rparams->end == $rparams->widget_id) {
		 $params[0]['position_close'] = "</div>";
	}

	$params[0]['before_widget'] = $params[0]['position_open'].$params[0]['before_widget'] ;
	$params[0]['after_widget'] = $params[0]['after_widget'] . $params[0]['position_close'];
	
	return $params;
}
~~~

A full override looks like the following:

~~~ .php
class GantryLayoutWidget_Standard extends GantryLayout {
	var $render_params = array(
		'gridCount'   => null,
		'prefixCount' => 0,
		'extraClass'  => ''
	);

	function render($params = array())
	{
		/** @global $gantry Gantry */
		global $gantry;
		$instance_params = $this->_getWidgetInstanceParams($params[0]['widget_id']);
		$chrome_to_use   = (isset($instance_params['widget_chrome']) && !empty($instance_params['widget_chrome'])) ? $instance_params['widget_chrome'] : $params[0]['chrome'];
		$params          = $gantry->renderLayout("chrome_" .$chrome_to_use, $params);

		$params[0]['position_open']  = '';
		$params[0]['position_close'] = '';

		$rparams   = $this->_getParams($params[0]);
		$start_tag = "";

		// see if this is the first widget in the postion
		if (property_exists($rparams, 'start') && $rparams->start == $rparams->widget_id) {
			$prefixClass = '';
			// get the prefix class for the start
			if ($rparams->widget_map[$rparams->position]['prefixCount'] != 0) {
				$prefixClass = " rt-prefix-" . $rparams->widget_map[$rparams->position]['prefixCount'];
			}
			ob_start();
			?>
		<div class="rt-grid-<?php echo $rparams->widget_map[$rparams->position]['paramsSchema'] . $prefixClass . $rparams->widget_map[$rparams->position]['extraClass']; ?>">
			<?php
			$start_tag                  = ob_get_clean();
			$params[0]['position_open'] = $start_tag;
		}

		if (property_exists($rparams, 'end') && $rparams->end == $rparams->widget_id) {
			$params[0]['position_close'] = "</div>";
		}

		$params[0]['before_widget'] = $params[0]['position_open'] . $params[0]['before_widget'];
		$params[0]['after_widget']  = $params[0]['after_widget'] . $params[0]['position_close'];

		return $params;
	}
}
~~~

Step 4: Adding Layout to Template
---------------------------------
Open up the templates index.php and find the widget position where we need to use the custom widget layout.

Edit the displayModules functions 2nd parameter to the name of your custom widget layout which was created in step 3. As seen in the example below:

~~~ .php
<?php echo $gantry->displayModules('top', 'example', 'standard'); ?>
~~~
