[<img src="https://hotio.dev/img/sonarr.png" alt="logo" height="130" width="130">](https://github.com/Sonarr/Sonarr)

[![GitHub Source](https://img.shields.io/badge/github-source-ffb64c?style=flat-square&logo=github&logoColor=white&labelColor=757575)](https://github.com/hotio/sonarr)
[![GitHub Registry](https://img.shields.io/badge/github-registry-ffb64c?style=flat-square&logo=github&logoColor=white&labelColor=757575)](https://github.com/orgs/hotio/packages/container/package/sonarr)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/sonarr?color=ffb64c&style=flat-square&label=pulls&logo=docker&logoColor=white&labelColor=757575)](https://hub.docker.com/r/hotio/sonarr)
[![Discord](https://img.shields.io/discord/610068305893523457?style=flat-square&color=ffb64c&label=discord&logo=discord&logoColor=white&labelColor=757575)](https://hotio.dev/discord)
[![Upstream](https://img.shields.io/badge/upstream-project-ffb64c?style=flat-square&labelColor=757575)](https://github.com/sonarr/sonarr)
[![Website](https://img.shields.io/badge/website-hotio.dev-ffb64c?style=flat-square&labelColor=757575)](https://hotio.dev/containers/sonarr)

## Starting the container

CLI:

```shell
docker run --rm \
    --name sonarr \
    -p 8989:8989 \
    -e PUID=1000 \
    -e PGID=1000 \
    -e UMASK=002 \
    -e TZ="Etc/UTC" \
    -e ARGS="" \
    -e DEBUG="no" \
    -v /<host_folder_config>:/config \
    hotio/sonarr
```

In most cases you'll need to add additional volumes, depending on your own personal preference, to get access to your files.

## Tags

| Tag                | Upstream        | Version | Build |
| -------------------|-----------------|---------|-------|
| `release` (latest) | master          | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fhotio%2Fsonarr%2Frelease%2FVERSION.json) | ![build](https://img.shields.io/github/workflow/status/hotio/sonarr/build/release?style=flat-square&label=) |
| `testing`          | develop         | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fhotio%2Fsonarr%2Ftesting%2FVERSION.json) | ![build](https://img.shields.io/github/workflow/status/hotio/sonarr/build/testing?style=flat-square&label=) |
| `nightly`          | phantom-develop | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fhotio%2Fsonarr%2Fnightly%2FVERSION.json) | ![build](https://img.shields.io/github/workflow/status/hotio/sonarr/build/nightly?style=flat-square&label=) |

You can also find tags that reference a commit or version number.

## Configuration location

Your sonarr configuration inside the container is stored in `/config/app`, to migrate from another container, you'd probably have to move your files from `/config` to `/config/app`.

## Executing your own scripts

If you have a need to do additional stuff when the container starts or stops, you can mount your script with the volume `/docker/host/my-script.sh:/etc/cont-init.d/99-my-script` to execute your script on container start or `/docker/host/my-script.sh:/etc/cont-finish.d/99-my-script` to execute it when the container stops. An example script can be seen below.

```shell
#!/usr/bin/with-contenv bash

echo "Hello, this is me, your script."
```

## Troubleshooting a problem

By default all output is redirected to `/dev/null`, so you won't see anything from the application when using `docker logs`. Most applications write everything to a log file too. If you do want to see this output with `docker logs`, you can set `DEBUG` to `yes`.
