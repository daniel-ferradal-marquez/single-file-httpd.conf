### Variables with Define

You can save some typing and repeating in the httpd configuration by defining variables from values that are used often. For that you can define them with directive `Define`, for example: `Define documentroot /var/www/html`, and then use the variable names you have defined later.

This makes furter name changes or even path changes easier later on or as a base to propagate to other path / names scenarios.

#### Reference

You can check the official source of all this information at [Define directive at the official httpd docs](http://httpd.apache.org/docs/current/mod/core.html#define).

See the included [httpd.conf](httpd.conf) to see how variables can be used in a configuration file to save time and repeating the same thing.
