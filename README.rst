
EXT:realurl 
==============================================

Reasons why this version performs better:

- Testcovered pagepath generation
- Languagevisibility compatible
- Optimized usage with multidomain setups
- Improved path-history handling

Upgrading from aoe_realurlpath
----------------------------------------------

- Change the pagepath renderer script to:

::

	'userFunc' => 'EXT:realurl/class.tx_realurl_pagepath.php:&tx_realurl_pagepath->main'

- Remove the tx_aoerealurlpath_overridesegment from the 'segTitleFieldList' setting

- Migrate the existing pagepath configuration:

::

  UPDATE pages SET tx_realurl_pathoverride = 0, tx_realurl_pathsegment = tx_aoerealurlpath_overridesegment,	tx_realurl_exclude = tx_aoerealurlpath_excludefrommiddle WHERE tx_aoerealurlpath_overridepath = '';
  UPDATE pages SET tx_realurl_pathoverride = 1, tx_realurl_pathsegment = tx_aoerealurlpath_overridepath, tx_realurl_exclude = tx_aoerealurlpath_excludefrommiddle WHERE  tx_aoerealurlpath_overridepath != '';
  UPDATE pages_language_overlay SET tx_realurl_pathoverride = 0, tx_realurl_pathsegment = tx_aoerealurlpath_overridesegment, tx_realurl_exclude = tx_aoerealurlpath_excludefrommiddle WHERE tx_aoerealurlpath_overridepath = '';
  UPDATE pages_language_overlay SET tx_realurl_pathoverride = 1, tx_realurl_pathsegment = tx_aoerealurlpath_overridepath, tx_realurl_exclude = tx_aoerealurlpath_excludefrommiddle WHERE tx_aoerealurlpath_overridepath != '';

