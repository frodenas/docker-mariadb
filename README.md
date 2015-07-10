# MariaDB Dockerfile

A Dockerfile that produces a Docker Image for [MariaDB](https://mariadb.com/).

## MariaDB version

The `master` branch currently hosts MariaDB 5.5.

Different versions of MariaDB are located at the github repo [branches](https://github.com/frodenas/docker-mariadb/branches).

## Usage

### Build the image

To create the image `frodenas/mariadb`, execute the following command on the `docker-mariadb` folder:

```
$ docker build -t frodenas/mariadb .
```

### Run the image

To run the image and bind to host port 3306:

```
$ docker run -d --name mariadb -p 3306:3306 frodenas/mariadb
```

The first time you run your container, a new user `admin` with all privileges will be created with a random password.
To get the password, check the logs of the container by running:

```
docker logs <CONTAINER_ID>
```

You will see an output like the following:

```
========================================================================
MySQL User: "admin"
MySQL Password: "mKHBsVb2i7OrY26K"
========================================================================
```

#### Credentials

If you want to preset credentials instead of a random generated ones, you can set the following environment
variables:

* `MYSQL_USERNAME` to set a specific username
* `MYSQL_PASSWORD` to set a specific password

On this example we will preset our custom username and password:

```
$ docker run -d \
    --name mariadb \
    -p 3306:3306 \
    -e MYSQL_USERNAME=myusername \
    -e MYSQL_PASSWORD=mypassword \
    frodenas/mariadb
```

#### Databases

If you want to create a database at container's boot time, you can set the following environment variables:

* `MYSQL_DBNAME` to create a database

On this example we will preset our custom username and password and we will create a database:

```
$ docker run -d \
    --name mariadb \
    -p 3306:3306 \
    -e MYSQL_USERNAME=myusername \
    -e MYSQL_PASSWORD=mypassword \
    -e MYSQL_DBNAME=mydb \
    frodenas/mariadb
```

#### Persist database data

The MariaDB server is configured to store data in the `/data` directory inside the container. You can map the
container's `/data` volume to a volume on the host so the data becomes independent of the running container:

```
$ mkdir -p /tmp/mariadb
$ docker run -d \
    --name mariadb \
    -p 3306:3306 \
    -v /tmp/mariadb:/data \
    frodenas/mariadb
```

## Copyright

Copyright (c) 2015 Ferran Rodenas. See [LICENSE](https://github.com/frodenas/docker-mariadb/blob/master/LICENSE) for details.
