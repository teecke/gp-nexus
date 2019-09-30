# Generic Platform - Nexus Service

## Overview

Teecke Generic Platform Nexus Service.

Docker-ompose simple configuration to bring up the Nexus service to the Generic Platform.

## Configuration

The service is formed by one container:

- **nexus**: based on [sonatype/nexus](https://hub.docker.com/r/sonatype/nexus/) docker image.

Use the `docker-compose.yml.sample` file as the source for your docker-compose configuration file.

## Operation

You must create a network called "platform_services" before start the services.

```console
docker network create platform_services
```

Then you can start the service with `docker-compose up -d` and stop it with `docker-compose stop` commands.

After the first run you can configure the service pointing a browser to <http://nexus:8081>

There is one volume created. All data and configuration are on this volumes, so never delete it.

```console
$ docker volume ls|grep "nexus\|VOLUME"
DRIVER              VOLUME NAME
DRIVER              VOLUME NAME
local               nexus_sonatype-work
```

There are also two tasks `cleanup` and `backup` that you can execute as stand-alone

```console
$ docker-compose exec nexus cleanup

[...]

$ docker-compose exec nexus backup
```

...or using [Teecke Generic Platform](https://github.com/teecke/generic-platform) project.

The backup data will be stored in the `/var/backups/gp/nexus/` directory of the container. You can copy the backup files with a simple "docker cp" command `docker cp $(docker-compose ps -q jenkins):/var/backups/gp gp`

## Known issues

None known
