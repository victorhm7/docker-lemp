## docker-lemp

> Do not use in Production.

A minimal single container LEMP stack for local development.

It is quick jumpstart for onboarding you into docker based development.

The docker container `adhocore/lemp` is composed of:

Name   | Version | Port
-------|---------|------
Alpine | 3.8     | -
PHP    | 7.3.1   | 9000
MySQL`*` | 5.7     | 3306
nginx  | 1.14.2  | 80

> `*`: It is actually MariaDB.

## Usage

Install [docker](https://docs.docker.com/install/) in your machine.
Also recommended to install [docker-compose](https://docs.docker.com/compose/install/).

```sh
# pull latest image
docker pull adhocore/lemp

# Go to your project root then run
docker run -p 8080:80 -v `pwd`:/var/www/html --name lemp -d adhocore/lemp

# In windows, you would use %cd% instead of `pwd`
docker run -p 8080:80 -v %cd%:/var/www/html --name lemp -d adhocore/lemp

# If you want to setup MySQL credentials, pass env vars
docker run -p 8080:80 -v `pwd`:/var/www/html -e MYSQL_ROOT_PASSWORD=1234567890 -e MYSQL_USER=dbuser -e MYSQL_PASSWORD=123456 -e MYSQL_DATABASE=appdb --name lemp -d adhocore/lemp
```

After running container as above, you will be able to browse [localhost:8080](http://localhost:8080)!

### Stop container

To stop the container, you would run:

```sh
docker stop lemp
```

### (Re)Start container

You dont have to always do `docker run` as in above unless you removed or lost your `lemp` container.

Instead, you can just start when needed:

```sh
docker start lemp
```

> **PRO** If you develop multiple apps, you can create multiple lemp containers with different names.
>
> eg: `docker run -p 8081:80 -v `pwd`:/var/www/html --name new-lemp -d adhocore/lemp`

### MySQL Default credentials

- **root password**: 1234567890 (if `MYSQL_ROOT_PASSWORD` is not passed)
- **user password**: 123456 (if `MYSQL_USER` is passed but `MYSQL_PASSWORD` is not)


### Nginx

URL rewrite is already enabled for you.
Either your app has `public/` folder or not, the rewrite adapts automatically.

