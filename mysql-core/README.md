# MYSQL for CORE Network Emulator

## Getting Started

First set the Container Image Name to fgftk/mysqlcore:latest (see figure)

![node.jpg](https://github.com/alehmannFRA-UAS/core-dockerfiles/blob/main/mysql-core/img/node.jpg?raw=true) 

Next open Services and choose UserDefined service. Create a shell script start.sh as depicted.

![userdefined.jpg](https://github.com/alehmannFRA-UAS/core-dockerfiles/blob/main/mysql-core/img/userDefined.jpg?raw=true)


#### Environment Variables

When you start the mysql image, you can adjust the configuration of the MySQL instance by passing one or more environment variables. These variables must passed by the start script, e.g., `export MYSQL_ROOT_PASSWORD=test`

`MYSQL_ROOT_PASSWORD` - This variable is mandatory and specifies the password that will be set for the MySQL root superuser account. In the above example, it was set to test.

`MYSQL_DATABASE` - This variable is optional and allows you to specify the name of a database to be created on image startup. If a user/password was supplied (see below) then that user will be granted superuser access (corresponding to GRANT ALL) to this database.

`MYSQL_USER, MYSQL_PASSWORD` - These variables are optional, used in conjunction to create a new user and to set that user's password. This user will be granted superuser permissions (see above) for the database specified by the MYSQL_DATABASE variable. Both variables are required for a user to be created. Do note that there is no need to use this mechanism to create the root superuser, that user gets created by default with the password specified by the MYSQL_ROOT_PASSWORD variable.

`MYSQL_ALLOW_EMPTY_PASSWORD` - This is an optional variable. Set to a non-empty value, like yes, to allow the container to be started with a blank password for the root user. NOTE: Setting this variable to yes is not recommended unless you really know what you are doing, since this will leave your MySQL instance completely unprotected, allowing anyone to gain complete superuser access.

`MYSQL_RANDOM_ROOT_PASSWORD` - This is an optional variable. Set to a non-empty value, like yes, to generate a random initial password for the root user (using pwgen). The generated root password will be printed to stdout (GENERATED ROOT PASSWORD: .....).

`MYSQL_ONETIME_PASSWORD` - Sets root (not the user specified in MYSQL_USER!) user as expired once init is complete, forcing a password change on first login. Any non-empty value will activate this setting. NOTE: This feature is supported on MySQL 5.6+ only. Using this option on MySQL 5.5 will throw an appropriate error during initialization.

`MYSQL_INITDB_SKIP_TZINFO` - By default, the entrypoint script automatically loads the timezone data needed for the CONVERT_TZ() function. If it is not needed, any non-empty value disables timezone loading.

## Dockerfile

* [GitHub](https://github.com/alehmannFRA-UAS/core-dockerfiles)

## License

View [license information](https://www.mysql.com/about/legal/) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
