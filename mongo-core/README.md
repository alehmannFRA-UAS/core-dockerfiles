# Mongo for CORE Network Emulator

## Getting Started

First set the Container Image Name to fgftk/mongocore:latest

Next open Services and choose UserDefined service. Create a shell script as depicted (example of another service).
Please replace with following: su mongodb -c "bash docker-entrypoint.sh mongod"

![userdefined.jpg](https://github.com/alehmannFRA-UAS/core-dockerfiles/blob/main/mysql-core/img/userDefined.jpg?raw=true)

Do not forget to set it as startup script in tab Startup/shutdown, e.g., sh startmongo.sh.

## Environment Variables

When you start the `mongo` image, you can adjust the initialization of the MongoDB instance by passing one or more environment variables on the `docker run` command line. Do note that none of the variables below will have any effect if you start the container with a data directory that already contains a database: any pre-existing database will always be left untouched on container startup.

### `MONGO_INITDB_ROOT_USERNAME`, `MONGO_INITDB_ROOT_PASSWORD`

These variables, used in conjunction, create a new user and set that user's password. This user is created in the `admin` [authentication database](https://docs.mongodb.com/manual/core/security-users/#user-authentication-database) and given [the role of `root`](https://docs.mongodb.com/manual/reference/built-in-roles/#root), which is [a "superuser" role](https://docs.mongodb.com/manual/core/security-built-in-roles/#superuser-roles).

The following is an example of using these two variables to create a MongoDB instance and then using the `mongo` cli to connect against the `admin` authentication database.

```console
$ docker run -d --network some-network --name some-mongo \
	-e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
	-e MONGO_INITDB_ROOT_PASSWORD=secret \
	mongo

$ docker run -it --rm --network some-network mongo \
	mongo --host some-mongo \
		-u mongoadmin \
		-p secret \
		--authenticationDatabase admin \
		some-db
> db.getName();
some-db
```

Both variables are required for a user to be created. If both are present then MongoDB will start with authentication enabled (`mongod --auth`).

Authentication in MongoDB is fairly complex, so more complex user setup is explicitly left to the user via `/docker-entrypoint-initdb.d/` (see the *Initializing a fresh instance* and *Authentication* sections below for more details).

### `MONGO_INITDB_DATABASE`

This variable allows you to specify the name of a database to be used for creation scripts in `/docker-entrypoint-initdb.d/*.js` (see *Initializing a fresh instance* below). MongoDB is fundamentally designed for "create on first use", so if you do not insert data with your JavaScript files, then no database is created.

## Docker Secrets

As an alternative to passing sensitive information via environment variables, `_FILE` may be appended to the previously listed environment variables, causing the initialization script to load the values for those variables from files present in the container. In particular, this can be used to load passwords from Docker secrets stored in `/run/secrets/<secret_name>` files. For example:

```console
$ docker run --name some-mongo -e MONGO_INITDB_ROOT_PASSWORD_FILE=/run/secrets/mongo-root -d mongo
```

Currently, this is only supported for `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD`.

# Initializing a fresh instance

When a container is started for the first time it will execute files with extensions `.sh` and `.js` that are found in `/docker-entrypoint-initdb.d`. Files will be executed in alphabetical order. `.js` files will be executed by `mongo` using the database specified by the `MONGO_INITDB_DATABASE` variable, if it is present, or `test` otherwise. You may also switch databases within the `.js` script.

## Dockerfile

* [GitHub](https://github.com/alehmannFRA-UAS/core-dockerfiles)

## License

View [license information](https://github.com/mongodb/mongo/blob/6ea81c883e7297be99884185c908c7ece385caf8/README#L89-L95) for the software contained in this image.

It is relevant to note the change from AGPL to SSPLv1 for all versions after October 16, 2018.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `mongo/` directory](https://github.com/docker-library/repo-info/tree/master/repos/mongo).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
