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