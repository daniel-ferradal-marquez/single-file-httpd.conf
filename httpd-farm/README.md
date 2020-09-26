<h1><b>Apache HTTPD Farms</b></h1>

In certain occassions the Administrator will need/prefer to make use of isolated Apache httpd instances, instead of a one global instance to handle all virtualhosts, this can be done sharing the same binaries or not as needed.

<br/>

<p><b>Reasons</b></p>
<p>Several reasons can apply to this:<p>
<p>
<ul>
<li>Different modules to load for each instance.</il>
<li>Different user for certain instances if needed.</il>
<li>Finetune the load allowed for each instance (MPM).</il>
<li>Completely isolated websites from one another.</il>
<li>Different binaries in the same machine.</il>
<li>Maybe certain instance needs a module that can't use the threaded MPM (event), so you define a separate instance for it and you don't need to burden the rest of the instances with a non-threaded MPM because one websites needs to be configured this way.</il>
</ul>
</p>

<p>The reasons can vary but if you propagate their paths correctly the benefits of having separate instances are obvious.</p>

<br/>
<p><b>What's needed</b></p>
<p>To do this all you need is define a good layout of paths to use so you don't end with a mess or confusion and you know where your instances reside. Dynamic paths such as logs , documentroot will go in a specific instance dir, while the binaries of your httpd installation don't have to be moved or touched.</p>

<p><b>As before, this is done in a single config file</b> (no riddled Include config mess).</p>

<p>The httpd.conf provided assumes main binary installation resides in /srv/apache/httpd (ServerRoot) but that can be changed/tweaked. There should be the typical subdirectories of a httpd installation bin/ lib/ modules/  ,etc.</p>

<p>And the different instances theirselves live with their own conf/ htdocs/ logs/ or whatever other directories you see fit in /web/instanceX/ to differenciate theirselves from the typical default installation paths and other instances and there are no conflicts once they are started. </p>

<p>It's very easy to script their generation this way. To create a new instance you just change the neccesary values at the top of the provided httpd.conf, and you can create many different instances easily this way, since changing parts are defined in variables on top.</p>

<br/>
<p>
<b>How to run these instances:</b>
<ul>
<li>Load a specific envvars file suited for each instance (if needed)</li>
<li>Run each instance in this fashion:<br/>
/srv/apache/httpd/bin/httpd -k [start|stop|graceful|graceful-stop|restart] -f /web/instance1/conf/instance1.conf</li>
</ul></p>

<br/>
<p><b>Why not just docker</b></p>
<p>Yes, why not? Some people prefer to issolate them using docker and some other people wont need or don't want to use docker, that's up to you.</p>

<br>
<p>As always, refer to httpd <a href="http://httpd.apache.org/docs">official docs</a> or the <a href="https://cwiki.apache.org/confluence/display/HTTPD">httpd wiki</a> for reliable info regarding how to configure httpd.</p>
