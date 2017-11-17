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

1. `git clone https://github.com/dynamic/silverstripe-docker.git ./`
Replace `./` if you wish to install into a sub directory

2. Run `docker network create reverse-proxy` to create the network all the docker containers will run on. (You will be prompted to do this if you skip this step)

## Commands

### new-dock
`new-dock <folder> [<url>]` creates a new docker-compose project folder. 
It requires a folder to create te project. This folder name will also be used in creating the containers.
The url is optional, and will default to using the folder name with `.dev` appended. `new-dock test t` will create a folder `test` and will be accesible with the url `t.dev`


### dock
The `dock` command will allow starting and stopping docker-compose setups

#### dock up
`dock up folder` will start a docker-compose in a specified folder. It will also start the reverse proxy and adminer containers.

#### dock halt
`dock halt [<folder>]` or `dock stop [<folder>]` will stop a docker-compose in a specified folder.
If no folder is specified all containers will be stopped.


## Webroot

Once your environment has been built, a `public` folder will be created in `folder`. Place your project files there.
If you are using silverstripe it is recommended to create a `silverstripe-cache` folder in `public`.

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

## SSH Access
use `docker ps` to find the container to ssh into. Usually its something like `folder_folder_web_1`.
### root
`docker exec -it <container_web_name> bash`
### www-data
`docker exec -it -u 1000 <container_web_name> bash`