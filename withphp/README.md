### PHP Processing

This method is the recommended nowadays to parse PHP files and present them in your webpage.
With this method Apache can use its best threaded MPM (event), while the PHP processing is handled by another server, php-fpm.

#### PHP-FPM 

[PHP-FPM](https://www.php.net/manual/en/install.fpm.php) is php's own daemon to parse your php scripts, separated from Apache and therefore without the need of the dated and limiting mod_php. In their own words "FPM (FastCGI Process Manager) is a primary PHP FastCGI implementation containing some features (mostly) useful for heavy-loaded sites. "

With this method Apache will reverse proxy php file requests to php-fpm, either to a unix socket file or to a tcp port.

#### Versatility

This method adds lots of versatility to your architecture also because you can separate them (Apache and PHP-FPM) in different machines or even if your php application is too heavy, to use several php-fpm backends and balance to them from Apache HTTPD. It also helps differentiate where a problem may be. 

Many users which rely on mod_php configurations think Apache HTTPD is slow, when it is their own php scripts causing that for many different reasons. Not to blame PHP in any way, just that often php applications like with any other programming language rely on the quality of the code in use, the backends it may be connecting to, etc.

Separating httpd process and php processing helps spotting where the problem is quicker to address the problem and define a solution.

#### Source of information

You should always check the documentation and updates in [mod_proxy_fcgi official docs](http://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html).
