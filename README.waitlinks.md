wait-links
==========

This script looks through the environment for variables that indicate that
there are services from other containers linked to this one.  It then sits in a
loop periodically checking each of those services to see if they are up.  This
lets you use it in startup script to avoid starting applications before their
dependencies are up (for example, use it from your web servers run script to
ensure that the database server is available before starting the web app).

It determines if they are up by attempting to open a connection to whatever TCP
or UDP ports they are exposing, so it will wait until the appropriate services
are actually listening before allowing the process to continue.

Author
======

2014 Jason Kohles <email@jasonkohles.com>

Part of the [docker-utils](http://github.com/jasonk/docker-utils) project.
