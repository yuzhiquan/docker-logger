# docker-logger [![Build Status](https://drone.umputun.com/api/badges/umputun/docker-logger/status.svg)](https://drone.umputun.com/umputun/docker-logger)

docker-logger is a small application collecting logs from other docker containers on the host. It can forward both stdout and stderr to local, rotated files and/or remote syslog.

## Install

Copy provided [`docker-compose.yml`](https://github.com/umputun/docker-logger/blob/master/docker-compose.yml), customize if needed and run is with `docker-compose up -d`

## Customization

All changes can be done via container's environment in `docker-compose.yml` or with command line

| Command line    | Environment   | Default                     | Description                               |
| --------------- | ------------- | --------------------------- | ----------------------------------------- |
| `--docker`      | `DOCKER_HOST` | unix:///var/run/docker.sock | docker host                               |
| `--syslog-host` | `SYSLOG_HOST` | 127.0.0.1:514               | syslog remote host                        |
| `--files`       | `LOG_FILES`   | No                          | enable logging to files                   |
| `--syslog`      | `LOG_SYSLOG`  | No                          | enable logging to syslog                  |
| `--max-size`    | `MAX_SIZE`    | 10                          | size of log triggering rotation (MB)      |
| `--max-files`   | `MAX_FILES`   | 5                           | number of rotated files to keep           |
| `--max-age`     | `MAX_AGE`     | 30                          | maximum number of days to retain          |
| `--exclude`     | `EXCLUDE`     |                             | excluded container names, comma separated |
|                 | `TIME_ZONE`   | UTC                         | Time zone for container                   |

- at least one of destinations (`files` or `syslog`) should be defined
- location of log files can be mapped to host via `volume`, ex: `- ./logs:/srv/logs` (see `docker-compose.yml`)
