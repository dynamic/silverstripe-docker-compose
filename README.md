# Docker-Compose for SilverStripe Development on Linux

Creates a reverse proxy and adminer container. Has commands to easily create a new silverstripe docker-compose instance.

It provides:
- NGINX Proxy
- Adminer
- SSL? (unsure if this works)

The template it creates provides:
- Apache
- PHP 7.1
- MySQL
- Composer
- SSPak

## Requirements

- [Docker](https://www.docker.com)

## Installation

1. `git clone -b linux https://github.com/dynamic/silverstripe-docker.git ./`
Replace `./` if you wish to install into a sub directory

2. Run `docker network create reverse-proxy` to create the network all the docker containers will run on. (You will be prompted to do this if you skip this step)

3. Make sure you ran through the [docker post install](https://docs.docker.com/engine/installation/linux/linux-postinstall/#manage-docker-as-a-non-root-user)

## Commands
Run `chmod +x dock` to make the commands executable.
you can run commands from the repo folder by pre-pending `./` to the `dock` command.
To run the commands normally add `cd /path/to/local/repo` just below `#!/bin/bash` in the `dock` file. Then run `cp dock /usr/bin/`.

### dock create
`dock create <folder> [<url>]` or `dock new <folder> [<url>]` creates a new docker-compose project folder. 
It requires a folder to create te project. This folder name will also be used in creating the containers.
The url is optional, and will default to using the folder name with `.dev` appended. `dock create test t` will create a folder `test` and will be accessible with the url `t.dev`

### dock up
`dock up <folder>` will start a docker-compose in a specified folder. It will also start the reverse proxy and adminer containers.

### dock ssh
`dock ssh <folder> [<user>]` will ssh into a web container. 
The specified folder does not need to be fully specified. If a docker-compose has a folder of `foobar`, `dock ssh foo` will find it.
The user is purely optional and will default to root (what docker uses). For the default decker-compose file generated it is recommended to use the use `1000` for sspaks.

### dock halt
`dock halt [<folder>]` or `dock stop [<folder>]` will stop a docker-compose in a specified folder.
If no folder is specified all containers will be stopped.


## Webroot

Once your environment has been built, a `public` folder will be created in `folder`. Place your project files there.
If you are using SilverStripe it is recommended to create a `silverstripe-cache` folder in `public`.

## Database Info

For SilverStripe projects:

```
# DB credentials
SS_DATABASE_SERVER="folder_db"
SS_DATABASE_USERNAME="root"
SS_DATABASE_PASSWORD=""
SS_DATABASE_NAME="yourproject"
```
The database name doesn't really matter all that much.

## Adminer
To use adminer add `127.0.0.1 adminer.dev  www.adminer.dev` to the hosts file. (`/etc/hosts` on Ubuntu)
Connecting to a database only requires the name of the database container. If the folder was name `test` the database container would be named `test_db`.
Adminer will store containers it connected to (and the username/password) until the actual container is removed.
The style can be changed by swapping out the `adminer.css` in the `public` folder.
