# Single File httpd.conf

**The intention** of this repository **is to show how to use a single configuration file to define all Apache HTTPD configuration** you may need as opposed of practically 100% of the other layouts offered out there.

### TLDR
**You can go ahead and check it here: [httpd.conf](httpd.conf)**

### Deeper explanation
- Most Linux distributions if not all come with a difficult complex scheme to configure Apache HTTPD Server.
Probably this configuration schemes were thought out mostly for ISP's which host lots of different virtualhosts for many different people. Although the purpose is clear, it confuses the heck of lots of users who do not really need such complex configuration schemes.

- I consider most configurations out there from tutorials can be misguiding.

- Here I just pretend to define a basic template configuration with every basic need within a single configuration file being also "production ready" at the same time, for example, including most security considerations regarding SSL and permissions.

- The aim for this are newbies and people who work on their own projects but this can serve as a starting template for much more.

- Unlike many other default configurations out there this one is meant to be used (or nearly) right away, without being filled with comments everywhere and straight to the point, full info is meant to be extracted directly from the official docs instead of random and probably misguiding tutorials out there or instead offering a cluttered configuration here.

- Of course everyone interested in learning how to configure apache should look at http://httpd.apache.org/docs/ for explanation of section/contexts and what every directive is for and where it should go. Apache documentation is very well organized and helpful, so do not forget to give it a try.

- Parts of the official docs that I recommend you to visit to understand how Apache works:

Contexts/Sections in HTTPD:
http://httpd.apache.org/docs/current/mod/directive-dict.html#Context

Core directives:
http://httpd.apache.org/docs/2.4/mod/core.html

Introduction to multi-processing-modules:
http://httpd.apache.org/docs/current/mpm.html

VirtualHost documentation:
http://httpd.apache.org/docs/2.4/vhosts/

SSL Howto:
http://httpd.apache.org/docs/current/ssl/ssl_howto.html

Security tips:
http://httpd.apache.org/docs/2.4/misc/security_tips.html


##### Ultra Minimal config by Apache HTTPD staff:
- https://cwiki.apache.org/confluence/display/HTTPD/Minimal+Config
