# Dockerfiles for CakePHP 4.x Installation 🥧

Basic docker configuration to setup ready to use CakePHP 4.x project.
This configuration can work as starting point for your own configuration.

## How to run

With [https://mutagen.io/](https://mutagen.io/) you can run this project with
the following command:

```sh
cd dockerfiles
sh build-mutagen-config
mutagen project start
```

The command `sh build-mutagen-config.sh` will create a `mutagen.yml` file in the
current directory with injected variables from the `.env` file (**this command
must be executed only onetime or when something changes in .env file**).

If you encounter problems during application bootstrap you can rebuild
docker infrastructure using this command:

```sh
docker compose up -d --build --force-recreate --remove-orphans
```

After that command you can restart mutagen:

```sh
mutagen project start
```

Using standard docker-compose.yml file you can run the project with the following
command:

```sh
docker compose up
```

## First setup

First time you need to run the following commands:

```sh
docker exec -it friendsofbabba_php bash
sh install.sh
```

Previous command will install full CakePHP 4.x stack.
After you have to inject environment variables in to config/app.php file.

## Environment Vars

You can use many environment variables to configure your project.

| Variable     | Description                                                         |
| ------------ | ------------------------------------------------------------------- |
| `APP_NAME`   | Application name, will be used as prefix for containers and volumes |
| `NGINX_HOST` | Application domain, will be used as default domain for containers   |
| `NGINX_POST` | Application port, will be used as default port for nginx containers |
| `DB_HOST`    | Database host, will be used as default host for database containers |
| `DB_PORT`    | Database port, will be used as default port for database containers |
| `DB_NAME`    | Database name, will be used as default name for database containers |
| `DB_USER`    | Database user, will be used as default user for database containers |
| `DB_PASS`    | Database password, will be used as default password for database    |

**You can customize** every aspect of your project by editing `dockerfiles/.env` file.
