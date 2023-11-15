# ZEROPS RECIPES

The concept of pre-prepared skeletons demonstrates the way how to set up and use technologies Zerops is supporting.

## phpMyAdmin 5.2.1

[phpMyAdmin](https://github.com/phpmyadmin/phpmyadmin) is a mature web-based administration tool for MariaDB and MySQL databases.

## Zerops import syntax

```yaml
#yamlPreprocessor=on
services:
  # Service will be accessible through zcli VPN under: http://phpmyadmin
- hostname: phpmyadmin
  # Type and version of a used service.
  type: php-apache@8.1+2.4
  # Whether the service will be run on one or multiple containers.
  # Since this is a utility service, using only one container is fine.
  minContainers: 1
  maxContainers: 1
  # Repository that contains phpMyAdmin code with build and deploy instructions.
  buildFromGit: https://github.com/zeropsio/recipe-phpmyadmin@main
  # Setting of the "DATABASE_HOSTNAME" environment variable.
  # It specifies the chosen hostname for the Zerops MariaDB service that should be managed.
  envVariables:
    # Here, the Zerops MariaDB service's chosen hostname is "mariadb".
    # Change it if you need to use a different one.
    DATABASE_HOSTNAME: mariadb
    # Used by phpMyAdmin for cookie based authentication to encrypt the cookie.
    SECRET_TOKEN: <@generateRandomString(<32>)>
```

Copy & paste the import snippet above into the dialog of **Import service** functionality.
