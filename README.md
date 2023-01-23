# Dockerfiles for CakePHP 4.x Installation 🥧

Basic docker configuration to setup ready to use CakePHP 4.x project.
This configuration can work as starting point for your own configuration.

**Notes**: the name `friendsofbabba` used in this configuration is just a suggestion
and must be referencing the env variable APP_NAME configured in `.env` file.

Suppose you have configured `hello_world` as your application name in `.env` file.
You will have these containers: hello_world_php, hello_world_web, hello_world_db,
use their names to reference them in your commands during installation.

## Prepare your project

To prepare your own CakePHP 4.x project you have to get a copy of this repository.

```sh
git clone git@github.com:RoBYCoNTe/friendsofbabba-dockerfiles.git yourprojectname
cd yourprojectname
rm -rf .git
```

## Environment Vars

Before start your own project you have to set some environment variables.
To do this you have to customize the following lines to your `.env` file:

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

## How to run

This project is configured to work with [https://mutagen.io/](https://mutagen.io/).

### Build mutagen configuration file

```sh
cd yourprojectname/dockerfiles
sh build-mutagen-config.sh
sh start.sh
```

### Run mutagen infrastructure

```sh
sh start.sh
```

**Notes**: previous command can take a while to run (be patient).

### Install CakePHP 4.x

```sh
docker exec -it friendsofbabba_php bash
composer create-project --prefer-dist cakephp/app:^4.3 /var/www/app --no-interaction
mv /var/www/app/* /var/www/html/
chown -R www-data:www-data /var/www/html
```

After this big step you will have to restore permission for the web container too:

```sh
docker exec -it friendsofbabba_web bash
chown -R www-data:www-data /var/www/html
```

**Notes**: mv command is necessary to move all files from the project root
to the web root and can take a while to be completed (because of mutagen sync).

### Configure database

Open the file `config/app_local.php` and change `Database` section like this:

```php
...
    'Datasources' => [
        'default' => [
            'host' => env('DB_HOST'),
            /*
             * CakePHP will use the default DB port based on the driver selected
             * MySQL on MAMP uses port 8889, MAMP users will want to uncomment
             * the following line and set the port accordingly
             */
            //'port' => 'non_standard_port_number',

            'username' => env('DB_USER'),
            'password' => env('DB_PASS'),
            'database' => env('DB_NAME'),
...
```

### Check your project

To check if everything is working open your browser and navigate
to configured NGINX_HOST in `.env` file. If something goes wrong open an issues,
I will try to help you.
