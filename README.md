docker-utils
============

This package contains some small shell scripts that make common startup tasks
(common for me, anyway) easier to deal with when building docker containers.

To use it, all you have to do is add the contents of the 'bin' directory to
your container (ideally somewhere in $PATH).

    % git clone http://github.com/jasonk/docker-utils
    % echo 'ADD docker-utils/bin /usr/local/bin/' >> Dockerfile

Requirements
============

This package is intended to be run inside a [Docker](http://docker.io)
container.

Some of the utility scripts make assumptions about the environment.  I've tried
to indicate in the documentation which utilities make these assumptions and
indicate how you can still use them if the assumptions aren't true.

Contents
========

These are the commands included in this package.  For more details on each, see
corresponding README.<command>.md file.

  * [secret](./README.secret.md) - Manage secret configuration information.
  * [template](./README.template.md) - Fill simple configuration templates
  * [waitlinks](./README.waitlinks.md) - Wait for linked services to be ready.

Author
======

2014 Jason Kohles <email@jasonkohles.com>

Part of the [docker-utils](http://github.com/jasonk/docker-utils) project.
