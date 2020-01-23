# Generic Platform - Nexus Service

## Overview

Docker image and docker-compose sample configuration to bring up a Nexus 3 Artifacts Service to the Teecke [Docker Generic Platform (GP)](https://github.com/teecke/docker-generic-platform).

## Configuration

The service is formed by one container:

- **nexus**: based on [sonatype/nexus](https://hub.docker.com/r/sonatype/nexus/) docker image.

## Operation

1. Configure the `/etc/security/limits.conf` on the docker host as it figures on the [Nexus 3](https://help.sonatype.com/repomanager3/system-requirements) System Requirements page:

    ```console
    $ tail /etc/security/limits.conf
    [...]

    nexus - nofile 65536
    ```

2. Use the `docker-compose.yml.sample` file as your docker-compose configuration file.

3. Create a docker network called "platform_services" before start the services with `docker network create platform_services`.

4. Install assets

    ```console
    $ devcontrol assets-install
    Generic Platform - Nexus Service (c) Teecke 2019-2020

    - Creating 'data' directory...[OK]
    - Setting 'data' permissions...[OK]
    - Creating 'data/nexus-data' directory...[OK]
    - Setting 'data/nexus-data' permissions...[OK]
    ```

5. Start with `docker-compose up -d`.

6. Open the url <http://localhost:8081> in a browser to access to the Nexus gui.

7. Manage backups of your files:

   1. Make a backup executing `docker-compose exec nexus backup`.
   2. Find the current backup within the `/var/backups/gp/nexus/` of the container.
   3. Extract the current backup executing `docker cp $(docker-compose ps -q nexus):/var/backups/gp gp`.

8. Stop the platform with `docker-compose stop`.

You can use this docker piece with the [Docker Generic Platform](https://github.com/teecke/docker-generic-platform) project.

## Known issues

None known
