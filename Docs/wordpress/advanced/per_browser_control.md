---
title: Per-Browser Specific Control

---

Per-Browser Specific Control
============================
The Gantry framework has the ability to load different CSS files based on which browser and operating system is viewing the template. This allows complete control over how a site is displayed to even the pickiest of browsers!

Every CSS file can be customized for different browser and operating system combinations with Gantry. This is handy for targeting specific browser issues, including IE6 compatibility. Each file is automatically loaded by the framework, depending on which browser/operating system is viewing the template.


How It Works
------------
Gantry looks for filenames based on the following mini-legend:

* __file__: Basename of CSS
* __browser__: [Firefox, Chrome, Safari, Opera, iPhone (works for both iPhone/iPod), iPad, Android, unknown]
* __engine__: [Trident, Gecko, WebKit, Presto, unknown]
* __longver__: The real long version of the browser (example, IE => 9.0, Safari 5 => 5.0.4, Firefox 5 => 5.0.0.20)
* __shortver__: The major version of the browser (example, if i'm running Safari 5.0.4 would be 5, if i'm running IE 9.0, would be 9)
* __platform__: [iPhone (worths for both iPhone/iPod), iPad, Android, mobile, Windows, OS X, Linux, unknown]


Possible Combinations
---------------------
* file.css
* file-**browser**.css
* file-**engine**.css
* file-**platform**.css
* file-**browser**-**platform**.css
* file-browser**shortver**.css [no space between the two]
* file-browser**longver**.css
* file-browser**shortver**-platform.css
* file-browser**longver**-platform.css


Real World Usage
----------------
Per-browser specific control works for **CSS files** only. For Gantry to lookup a specific file based on your browser, there must be a reference to the base CSS file using the Gantry `$gantry->addStyle();` or the output CSS file of the `$gantry->addLess();` method. In pre-Gantry 4 templates, there was always a reference to load `template.css`. So, you could use `template-ie8.css` to target **IE8** or `template-chrome-win.css` if you needed to target **Chrome on Windows** file.

In Gantry 4 templates, there is a special case that enables a custom CSS file to be manually created: `[TEMPLATE]/css/[TEMPLATE]-custom.css`. This file, if found, will automatically be added. You can also use per-browser options on this file. For example: `[TEMPLATE]/css/[TEMPLATE]-custom-trident.css`.


Real-World Example
------------------
In the **default gantry template**, there is a `global.less` file that is compiled and output to a `master.css` file. If you were using Chrome v.21 on OS X, Gantry would automatically look for the following files in your `[TEMPLATE]/css/` folder:

* master.css
* master-chrome.css
* master-mac.css
* master-webkit.css
* master-chrome-mac.css
* master-chrome21.css
* master-chrome21.0.1180.82.css
* master-chrome21-mac.css
* master-chrome21.0.1180.82-mac.css
