# Docker Setup for SilverStripe

This project contains files to get up and running with Docker Machine. It uses VirtualBox to spin up a small Linux machine to run your Docker containers.

## Requirements


- [Docker Toolbox](https://www.docker.com/products/docker-toolbox)


## Create A Machine

Below, subsititue `projectname` with the neme of your project.

Create a new machine for your project:

`docker-machine create --driver virtualbox projectname`

## Use a Machine

To use a previously created machine:

`docker-machine start projectname`

Tell Docker to talk to the new machine:

`docker-machine env projectname`

Connect your shell to the new machine:

`eval "$(docker-machine env projectname)"`

In terminal, bring the Docker containers up:

`docker-compose build` (only if a new project)

`docker-compose up -d`

Get the machine IP:

`docker-machine ip projectname`

In your browser, navigate to the IP returned about, port `8080`

`http://192.168.99.100:8080`

## Stop a Machine

`docker-compose stop`

`docker-machine stop projectname`

## Database Info

For SilverStripe projects:

```
# DB credentials
SS_DATABASE_SERVER="database"
SS_DATABASE_USERNAME="root"
SS_DATABASE_PASSWORD=""
SS_DATABASE_NAME="yourproject"
```

## SSH Access

`docker exec -it projectname_web_1 bash`