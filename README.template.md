template
========
A very simple templating program that allows you to fill-in configuration
templates as necessary.  To use it, you just call it before starting your
service.  With runit you can do this from your services run script:

    % cat <<END > /etc/services/apache/run
    #!/bin/sh
    # runit run script
    template /etc/httpd.conf.tmpl
    exec httpd -DNO_DETACH
    END
    chmod +x /etc/services/apache/run

You could also do this from the baseimage startup directory:

    % cat <<END > /etc/my_init.d/501-apache-config
    #!/bin/sh
    # my_init startup script
    template --once /etc/httpd.conf.tmpl /etc/httpd.conf
    END
    chmod +x /etc/my_init.d/501-apache-config

Generally you only need to provide either the name of a configuration file (in
which case the script will assume the template is the same name with '.tmpl'
appended), or the name of the template (if the argument already ends with
.tmpl, then the script will remove that to get the name of the configuration
file to build).

If you provide the argument '--once' then the configuration file will not
be rebuilt if it already exists.

The template file isn't technically a template, it is just text that will be
loaded into an 'echo <<END' block, which will result in variable substitution
being done on it the same a shell script.  The upside is that this makes it a
very simple, yet still very powerful format.  The downside is that you have to
escape any characters that the shell would otherwise interpret (such as dollar
signs).

### Example wp-config.php template ###
    /** WordPress Configuration */
    /* This gets the MySQL database address from the docker link */
    define( 'DB_HOST', '$DB_PORT_6379_TCP_ADDR' );
    /* This gets the database information from the environment */
    /* It was probably put there by a docker builder of some kind. */
    define( 'DB_NAME', '$DB_DATABASE_NAME' );
    define( 'DB_USER', '$DB_DATABASE_USER' );
    define( 'DB_PASSWORD', '$DB_DATABASE_PASSWORD' );

Author
======

2014 Jason Kohles <email@jasonkohles.com>

Part of the [docker-utils](http://github.com/jasonk/docker-utils) project.
