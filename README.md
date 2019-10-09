# Generic Platform - Nexus Service

## Overview

Docker image and docker-compose sample configuration to bring up a Nexus Artifacts Service to the Teecke [Docker Generic Platform (GP)](https://github.com/teecke/docker-generic-platform).

## Configuration

The service is formed by one container:

- **nexus**: based on [sonatype/nexus](https://hub.docker.com/r/sonatype/nexus/) docker image.

## Operation

1. Use the `docker-compose.yml.sample` file as your docker-compose configuration file.

2. Create a docker network called "platform_services" before start the services with `docker network create platform_services`.

3. Create a directory called `sonatype-work` to store the nexus configuration and artifact file.

4. Start with `docker-compose up -d`.

5. Open the url <http://localhost:8081> in a browser to access to the Nexus gui.

6. Manage backups of your files:

   1. Make a backup executing `docker-compose exec nexu backup`.
   2. Find the current backup within the `/var/backups/gp/nexus/` of the container.
   3. Extract the current backup executing `docker cp $(docker-compose ps -q nexus):/var/backups/gp gp`.

7. Stop the platform with `docker-compose stop`.

You can use this docker piece with the [Docker Generic Platform](https://github.com/teecke/docker-generic-platform) project.

## Known issues

None known
