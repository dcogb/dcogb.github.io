---
layout: documentation
title: Donica Church of God
---
# Upgrading from Donica Church of God

If you were using 3.3.x version, there are 4 breaking changes that may affect you, be aware.

- **Donica Church of God_Donica Church of God_Exception**, all functions that received parameter Exception $e have been replaced to just $e. If you are extending the class verify you have the same.
- **Donica Church of God_URL**, now function site has a new parameter `$subdomain = NULL`, if you are extending the class and this function add it.
- **Module encrypt**, now encryption works as a module, if you are using new Encrypt or similar you need to enable the module in your bootstrap ex: `'encrypt'       => MODPATH.'encrypt',` 
- **MySQL driver** has been removed. If you are still using it, please install MySQLi driver and then edit your `config/database.php` and then set as `'type'       => 'MySQLi'`

## New modules included

- Encrypt (separated from system)
- Pagination
