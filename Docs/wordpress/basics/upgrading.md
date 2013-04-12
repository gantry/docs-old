---
title: Upgrading

---

Upgrading
=========

Upgrading the Gantry Framework plugin is a relatively striaghtforward and simple process. This can be done using the built-in WordPress updater. Go to **Admin Dashboard → Updates**, select **Check Again** to load all available updates. Then check the checkbox next to the Gantry Template Framework and click **Update Plugins**.. Gantry will now be updated directly from the web.

![](assets/upgrading-update.jpg)

Alternatively, you can upload the updated version via FTP. You would just need to download the latest [Gantry files][files], extract them and overwrite the whole `gantry` directory under `wp-content/plugins`. There is no need to uninstall first, as the files will be overwritten durning the FTP upload.

You can check to see if the correct Gantry version has been installed by going to **Plugins** and searching for Gantry. The version number will appear in the resulting table.


[files]: http://code.google.com/p/gantry-framework/downloads/list?can=3&q=platform%3DWordPress
