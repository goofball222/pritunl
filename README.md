# Pritunl Docker Container

[![Latest Build Status](https://github.com/goofball222/pritunl/actions/workflows/build-latest.yml/badge.svg)](https://github.com/goofball222/pritunl/actions/workflows/build-latest.yml) [![Docker Pulls](https://img.shields.io/docker/pulls/goofball222/pritunl.svg)](https://hub.docker.com/r/goofball222/pritunl/) [![Docker Stars](https://img.shields.io/docker/stars/goofball222/pritunl.svg)](https://hub.docker.com/r/goofball222/pritunl/) [![License](https://img.shields.io/github/license/goofball222/pritunl.svg)](https://github.com/goofball222/pritunl)

## Docker tags:
| Tag | pritunl Version | Description | Release Date |
| --- | :---: | --- | :---: |
| [latest](https://github.com/goofball222/pritunl/blob/main/stable/Dockerfile) | v1.30.3157.70 | Latest stable release | 2022-05-05 |

---

* [Recent changes, see: GitHub CHANGELOG.md](https://github.com/goofball222/pritunl/blob/main/CHANGELOG.md)
* [Report any bugs, issues or feature requests on GitHub](https://github.com/goofball222/pritunl/issues)

---

## Description

Pritunl container built on Alpine Linux. Supports IPv6 and running behind a reverse proxy. This container requires an external Mongo DB and should be run via Docker Compose or other orchestration.

---

## Usage

This container exposes the following five ports:
* `80/tcp` pritunl web server http port (standalone mode)
* `443/tcp` pritunl web server https port (standalone and wireguard reverse-proxy mode)
* `1194/tcp` pritunl VPN service port
* `1194/tcp` pritunl OpenVPN service port
* `1195/udp` pritunl wireguard service port - No default in app, this is a suggestion only.
* `9700/tcp` pritunl web server http port (non-wireguard reverse-proxy mode)

---

**Wireguard**

The Docker host is required to have wireguard kernel modules installed and loaded.

Wireguard also requires that the pritunl web service exists internally on port 443 with SSL enabled (self-signed or LetsEncrypt cert). Without this clients will fail to connect or connection will time out after 15s in wireguard mode. This presents problems with existing reverse-proxy support using port 9700 and no SSL.

Wireguard + Traefik 1.X reverse-proxy + pritunl SSL self-signed cert:
* Set `InsecureSkipVerify = true` in Traefik 1.X `traefik.toml` config file (configure Traefik to accept invalid/self-signed certs)
* Set container ENV variable `REVERSE_PROXY=true` (configure pritunl for reverse-proxy/load-balance mode)
* Set container ENV variable `WIREGUARD=true` (configure pritunl to run web interface on port 443 with SSL)

Further pritunl wireguard information available at:
* https://docs.pritunl.com/docs/wireguard
* https://docs.pritunl.com/docs/wireguard-client

---

**OpenVPN server fails to start, insmod error**

`ip6tables v1.8.3 (legacy): can't initialize ip6tables table 'filter': Table does not exist (do you need to insmod?)` is repeatedly logged in the Docker container log along with python errors.

Load the ip6tables_filter kernel module on your Docker host and restart the container:

```bash
user@host:~$ sudo modprobe ip6table_filter
user@host:~$ sudo docker restart pritunl
```

This may need to be performed after kernel upgrades and reboots on the Docker host.
* https://ilhicas.com/2018/04/08/Fixing-do-you-need-insmod.html

---

**Basic docker-compose.yml to launch a Mongo DB container instance, pritunl in standalone mode, and make the web and VPN ports accessible**

```bash

version: '3'

services:
  mongo:
    image: mongo:latest
    container_name: pritunldb
    hostname: pritunldb
    network_mode: bridge
    volumes:
      - ./db:/data/db

  pritunl:
    image: goofball222/pritunl:latest
    container_name: pritunl
    hostname: pritunl
    depends_on:
        - mongo
    network_mode: bridge
    privileged: true
    sysctls:
      - net.ipv6.conf.all.disable_ipv6=0
    links:
      - mongo
    volumes:
      - /etc/localtime:/etc/localtime:ro
    ports:
      - 80:80
      - 443:443
      - 1194:1194
      - 1194:1194/udp
      - 1195:1195/udp
    environment:
      - TZ=UTC

```

---

**Other/extended docker-compose.yml examples see: https://github.com/goofball222/pritunl/tree/main/examples**

---

**Environment variables:**

| Variable | Default | Description |
| :--- | :---: | --- |
| `DEBUG` | ***false*** | Set to *true* for extra entrypoint script verbosity for debugging |
| `MONGODB_URI` | ***mongodb://mongo:27017/pritunl*** | Sets the URI Pritunl will access for the Mongo DB instance |
| `PRITUNL_OPTS` | ***unset*** | Any additional custom run options for the container pritunl process
| `REVERSE_PROXY` | ***false*** | Set to *true* to set the pritunl web interface to run in reverse-proxy mode (Traefik/nginx) |
| `WIREGUARD` | ***false*** | Set to *true*, Switches web interface back to port 443 and HTTPS if running wireguard with reverse-proxy (Traefik/nginx) |

[//]: # (Licensed under the Apache 2.0 license)
[//]: # (Copyright 2018 The Goofball - goofball222@gmail.com)
