secret
======

The 'secret' script is a little utility script (generally used from within
templates) that allows you to automatically generate secret values.  These are
often used for things like hashing keys, shared secrets, or even automatically
generated passwords.

To use 'secret', just run it with an argument indicating the name of the
secret.  If a secret was already generated with that name then it will be
returned, otherwise a new secret will be generated (using pwgen) and stored
(by default in the directory /etc/secrets, you can change this by setting
the location you want it stored in the environment:

    export DOCKER_BOOT_UTILS_SECRETS=/home/secrets-user/my-secrets

If you pass any additional arguments to 'secret' beyond just the secret name,
they will be passed verbatim to 'pwgen'.  So, for example, you can pass a
number in order to specify a length, or flags to indicate the type of
characters to include'.

    % echo "root:$(secret root-password 12)" | chpasswd

    # Another Wordpress wp-config.php example
    # See http://github.com/jasonk/docker-utils/README.template.md
    define( 'AUTH_KEY',         '$(secret WORDPRESS_AUTH_KEY -s 64)' );
    define( 'SECURE_AUTH_KEY',  '$(secret WORDPRESS_SECURE_AUTH_KEY -s 64)' );
    define( 'LOGGED_IN_KEY',    '$(secret WORDPRESS_LOGGED_IN_KEY -s 64)' );
    define( 'NONCE_KEY',        '$(secret WORDPRESS_NONCE_KEY -s 64)' );
    define( 'AUTH_SALT',        '$(secret WORDPRESS_AUTH_SALT -s 64)' );
    define( 'SECURE_AUTH_SALT', '$(secret WORDPRESS_SECURE_AUTH_SALT -s 64)' );
    define( 'LOGGED_IN_SALT',   '$(secret WORDPRESS_LOGGED_IN_SALT -s 64)' );
    define( 'NONCE_SALT',       '$(secret WORDPRESS_NONCE_SALT -s 64)' );

Author
======

2014 Jason Kohles <email@jasonkohles.com>

Part of the [docker-utils](http://github.com/jasonk/docker-utils) project.

