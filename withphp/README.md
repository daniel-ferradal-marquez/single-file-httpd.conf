<b>PHP Processing</b>

<p>This method is the recommended one noadays to parse PHP files and present them in your webpage.
With this method Apache can use its best threaded MPM (event), while the PHP processing is handled by another server, php-fpm.</p>


<b>PHP-FPM</b> 

<p>PHP-FPM is php's own daemon to parse your php scripts, separated from Apache and therefore without the need of the dated and limiting mod_php.

With this method Apache will reverse proxy php file requests to php-fpm, either to a unix socket file or to a tcp port.</p>

<b>Versatility</b>

<p>This method adds lots of versatility to your architecture also because you can separate them (Apache and PHP-FPM) in different machines or even if your php application is too heavy, to use several php-fpm backends and balance to them from Apache HTTPD.</p>

<b>Source of information</b>

<p>You should always check the documentation and updates in <a href="http://httpd.apache.org/docs/current/mod/mod_proxy_fcgi.html">mod_proxy_fcgi official docs</a>

