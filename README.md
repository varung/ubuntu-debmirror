# debmirror

<p align="center">
    <a href="https://travis-ci.com/flavienbwk/debmirror.svg?branch=master" target="_blank">
        <img src="https://travis-ci.com/flavienbwk/debmirror.svg?branch=master"/>
    </a>
</p>

Dockerized [debmirror](https://help.ubuntu.com/community/Debmirror) script for mirroring + serving

Status : tested & working :heavy_check_mark:</p>

TL;DR : This repository allows you to create & update your own Ubuntu or Debian mirror. You can then use it offline.

## Downloading & updating

1. Edit the `mirrorbuild.sh` file at your convenience

2. Run the `mirror` container :

    ```bash
    docker-compose build
    docker-compose up mirror
    ```

    > This repository is shipped with the Ubuntu 22.04 default configuration

3. (optional) Add a CRON job to keep your mirror up to date :

    After typing `crontab -e` in your shell, add :

    ```cron
    0 */12 * * * docker-compose -f /path/to/debmirror/docker-compose.yml up mirror > /path/to/debmirror/logs/cron.log 2>&1
    ```

    > This CRON job will run every 12th hour

## Serving

1. Check your mirroring succeeded in `./mirror/mirror/*` or typing `du -sh ./mirror`

    _If this directory is at least 130G, you can consider it worked._

2. Run the server :

    ```bash
    docker-compose up -d server
    ```

    Server will run on [`localhost:8080`](http://localhost:8080)  

:point_right: Feel free to add a reverse proxy or update the [nginx configuration file](./nginx.conf) to secure the mirror with SSL/TLS  
:point_right: Feel free to send **pull requests** as well !
