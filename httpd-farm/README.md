### Apache HTTPD Farms

In certain occassions the Administrator will need/prefer to make use of isolated Apache httpd instances, instead of a one global instance to handle all virtualhosts, this can be done sharing the same binaries or not as needed.

#### Reasons
Several reasons might apply to this:

- Different modules to load for each instance.
- Different user for certain instances if needed.
- Finetune the load allowed for each instance (MPM).
- Completely isolated websites from one another.
- Different binaries in the same machine.
- Maybe certain instance needs a module that can't use the threaded MPM (event), so you define a separate instance for it and you don't need to burden the rest of the instances with a non-threaded MPM because one websites needs to be configured this way.

The reasons can vary but if you propagate their paths correctly the benefits of having separate instances are obvious.

#### What's needed
To do this all you need is define a good layout of paths to use so you don't end with a mess or confusion and you know where your instances reside. Dynamic paths such as logs , documentroot will go in a specific instance dir, while the binaries of your httpd installation don't have to be moved or touched.

**As before, this is done in a single config file** (no riddled Include config mess).

The `httpd.conf` provided assumes main binary installation resides in `/srv/apache/httpd (ServerRoot)` but that can be changed/tweaked. There should be the typical subdirectories of a httpd installation bin/ lib/ modules/  ,etc.

And the different instances theirselves live with their own conf/ htdocs/ logs/ or whatever other directories you see fit in /web/instanceX/ to differenciate theirselves from the typical default installation paths and other instances and there are no conflicts once they are started. 

It's very easy to script their generation this way. To create a new instance you just change the neccesary values at the top of the provided `httpd.conf`, and you can create many different instances easily this way, since changing parts are defined in variables on top.

#### How to run these instances:

- Load a specific envvars file suited for each instance (if needed)
- Run each instance in this fashion:
`/srv/apache/httpd/bin/httpd -k [start|stop|graceful|graceful-stop|restart] -f /web/instance1/conf/instance1.conf`.

###### Note that, before executing httpd binary you may need to load certain system variables first, like `LD_LIBRARY_PATH` in certain scenarios. Apache HTTPD usually includes a file called envvars in bin/ directory precisely for this, and this is why usually in many distributions including default httpd layout a script to invoke httpd called `apachectl` is used.

#### Why not just docker/podman/container?
Yes, why not? Some people prefer to issolate them using docker and some other people wont need or don't want to use docker, that's up to you.

As always, refer to httpd [official docs](http://httpd.apache.org/docs) or the [httpd wiki](https://cwiki.apache.org/confluence/display/HTTPD) for reliable info regarding how to configure httpd.
