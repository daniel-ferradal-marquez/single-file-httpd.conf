<b>Single Config File for Docker</b>

<p>I generally find Docker very useful to try server software without installing anything. Sometimes you may want to test in a docker container and just remove it afterwards, or have a more permanent solution with Docker.</p>

<p>For this case I am going to show a small guide on how to use a single file httpd configuration (this time the one we explained with variables in another directory) with Docker to avoid complicatons or even to do a quick test without going crazy</p>

<p>In this case I am going to test with image httpd:2.4.46-alpine (current latest with alpine OS).

<p>You start by downloading it in your system with docker, for example:</p>
<li>docker pull httpd:2.4.46-alpine</li>

<p>Then you decide a <b>directory structure</b> where you will have configuration, logs and documentroot.</p>
<p>For Example:</p>
<p>
<li>/srv/httpd</li>
<li>/srv/httpd/conf</li>
<li>/srv/httpd/logs</li>
<li>/srv/httpd/htdocs</li>
</p>

<p>You copy the httpd.conf I provide in "/srv/httpd/conf", I also like to get mime.types from the server and copy it to the conf directory I will use in my system:</p>
<p>
<li>docker run --rm httpd:2.4.46-alpine cat /usr/local/apache2/conf/mime.types > /srv/httpd/conf/mime.types</li>
</p>

<p>To set up SSL you will at least have to use a certificate. You can complete the provided configuration with mod_md to autoget them from let's encrypt, or make a self-signed if you want to do a quick test.</p>

<p>For example, to make a self-signed you can run something like:</p>

<p>
<li>openssl req -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout server.key -out server.crt</li>
<li>once you have the files copy server.key and server.crt in /srv/httpd/conf</li>
</p>

<p>Last you can create a index.html for testing and place it in /srv/httpd/htdocs</p>
<p>
<li>echo "It Works!" > /srv/httpd/htdocs/index.html</li>
</p>

<p>You are all set, now fire up a container, I for example test with non-used ports, 8090 for http and 4443 for https:</p>
<p>
<li>docker run -d -p 8090:80 -p 4443:443 --name httpd-tests -v /srv/httpd/conf:/usr/local/apache2/conf -v /srv/httpd/logs:/usr/local/apache2/logs -v /srv/httpd/htdocs:/usr/local/apache2/htdocs httpd:2.4.46-alpine</li>
<p>With this you are binding apache to any ip in your server and port 8090 and 4443 (for SSL), you can access your server then with http://127.0.0.1:8090 or https://127.0.0.1:4443. You can use other ports or ips in your server of course just make sure no other service is using the same combination or ip:port.</p>
</p>


<p><b>Reference</b></p>


<p>You can check the official source for all things httpd at the <a href="http://httpd.apache.org/docs/current">HTTPD Current Documentation page</a>

<p>Credit for SSL global configuration goes to: <a href="https://ssl-config.mozilla.org/#server=apache&version=2.4.46&config=intermediate&openssl=1.1.1k&guideline=5.6">Mozilla SSL Configurator</a>. I generally have a clear picture of what I want to set but the selection of ciphers is always a pain and this configurator helps getting that out of the way in cases where you want to use a more or less secure and correct setup quickly.</p>
