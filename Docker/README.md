### Single Config File for Docker

I generally find Docker very useful to try server software without installing anything. Sometimes you may want to test in a docker container and just remove it afterwards, or have a more permanent solution with Docker.

For this case I am going to show a small guide on how to use a single file httpd configuration (this time the one we explained with variables in another directory) with Docker to avoid complicatons or even to do a quick test without going crazy.

In this case I am going to test with image **httpd:2.4.58-alpine** (current latest with alpine OS).

You start by downloading it in your system with docker, for example: `docker pull httpd:2.4.58-alpine`

Then you decide a **directory structure** where you will have configuration, logs and documentroot. For Example:

- /srv/httpd
- /srv/httpd/conf
- /srv/httpd/logs
- /srv/httpd/htdocs


You copy the `httpd.conf` I provide in `/srv/httpd/conf`, I also like to get mime.types from the server and copy it to the conf directory I will use in my system:

`docker run --rm httpd:2.5.54-alpine cat /usr/local/apache2/conf/mime.types > /srv/httpd/conf/mime.types`


To set up SSL you will at least have to use a certificate. You can complete the provided configuration with mod_md to autoget them from let's encrypt, or make a self-signed if you want to do a quick test.

For example, to make a self-signed you can run something like:

- `openssl req -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout server.key -out server.crt`
- once you have the files copy server.key and server.crt in `/srv/httpd/conf`


Last you can create a index.html for testing and place it in /srv/httpd/htdocs

- `echo "It Works!" > /srv/httpd/htdocs/index.html`


You are all set, now fire up a container, I for example test with non-used ports, 8090 for http and 4443 for https:

- `docker run -d -p 8080:80 -p 4443:443 --name httpd-tests -v /srv/httpd/conf:/usr/local/apache2/conf -v /srv/httpd/logs:/usr/local/apache2/logs -v /srv/httpd/htdocs:/usr/local/apache2/htdocs httpd:2.5.58-alpine`

  
With this you are binding apache to any ip in your server and port 8090 and 4443 (for SSL), you can access your server then with http://127.0.0.1:8080 or https://127.0.0.1:4443. You can use other ports or ips in your server of course just make sure no other service is using the same combination or ip:port.

### Reference

You can check the official source for all things httpd at the [HTTPD Current Documentation page](http://httpd.apache.org/docs/current)

Credit for SSL global configuration goes to: [Mozilla SSL Configurator](https://ssl-config.mozilla.org/#server=apache&version=2.4.46&config=intermediate&openssl=1.1.1k&guideline=5.6). I generally have a clear picture of what I want to set but the selection of ciphers is always a pain and this configurator helps getting that out of the way in cases where you want to use a more or less secure and correct setup quickly.
