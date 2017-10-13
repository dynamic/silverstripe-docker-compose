# Docker-Compose for SilverStripe Development

An apache and PHP 7.1 server. Intended for use with docker-compose.

It provides:

- Apache
- PHP 7.1
- MySQL
- Composer
- SSPak

## Requirements

- [Docker](https://www.docker.com)

## Installation

`git clone https://github.com/dynamic/silverstripe-docker.git yourproject`

## Usage

From the directory `yourproject `:

`docker-compose up -d`

if you wish to disable the web and database containers from running at startup change `restart: always` to one of the following:
```
restart: "no"
restart: always
restart: on-failure
restart: unless-stopped
```
[More information on restart policies.](https://blog.codeship.com/ensuring-containers-are-always-running-with-dockers-restart-policy/)

Your site will be visible at [http://localhost:8080](http://localhost:8080)

### Webroot

Once your environment has been built, a `public` folder will be created in `yourproject`. Place your project files there.

### Database Info

For SilverStripe projects:

```
# DB credentials
SS_DATABASE_SERVER="database"
SS_DATABASE_USERNAME="root"
SS_DATABASE_PASSWORD=""
SS_DATABASE_NAME="yourproject"
```

### SSH Access

`docker exec -it yourproject_web_1 bash`

### Ubuntu/Linux caveats
[Images not being resampled/resized](https://serversforhackers.com/c/dckr-file-permissions)
  - You may need to delete the session file in the docker container
