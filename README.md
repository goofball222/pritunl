# Pritunl Docker Container

[![Docker Build Status](https://img.shields.io/docker/build/goofball222/pritunl.svg)](https://hub.docker.com/r/goofball222/pritunl/) [![Docker Pulls](https://img.shields.io/docker/pulls/goofball222/pritunl.svg)](https://hub.docker.com/r/goofball222/pritunl/) [![Docker Stars](https://img.shields.io/docker/stars/goofball222/pritunl.svg)](https://hub.docker.com/r/goofball222/pritunl/) [![MB Layers](https://images.microbadger.com/badges/image/goofball222/pritunl.svg)](https://microbadger.com/images/goofball222/pritunl) [![MB Commit](https://images.microbadger.com/badges/commit/goofball222/pritunl.svg)](https://microbadger.com/images/goofball222/pritunl) [![MB License](https://images.microbadger.com/badges/license/goofball222/pritunl.svg)](https://microbadger.com/images/goofball222/pritunl)

## Docker tags:
| Tag | pritunl Version | Description | Release Date |
| --- | :---: | --- | :---: |
| [latest](https://github.com/goofball222/pritunl/blob/master/stable/Dockerfile) | 1.29.1827.6 | Latest stable release | 2018-09-13 |

---

* [Recent changes, see: GitHub CHANGELOG.md](https://github.com/goofball222/pritunl/blob/master/CHANGELOG.md)
* [Report any bugs, issues or feature requests on GitHub](https://github.com/goofball222/pritunl/issues)

---

## Description

Pritunl container built on Alpine Linux. Supports IPv6 and running behind a reverse proxy. This container requires an external Mongo DB and should be run via Docker Compose or other orchestration.

---

## Usage

This container exposes the following five ports:
* `80/tcp` pritunl web server http port (standalone mode)
* `443/tcp` pritunl web server https port (standalone mode)
* `1194/tcp` pritunl VPN service port
* `1194/udp` pritunl VPN service port
* `9700/tcp` pritunl web server http port (reverse-proxy mode)

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
    environment:
      - TZ=UTC

```

---

**Extended docker-compose.yml to launch the DB, pritunl in reverse-proxy mode, and add labels for Traefik**

```bash

version: '3'

services:
  mongo:
    image: mongo:latest
    container_name: pritunldb
    hostname: pritunldb
    networks:
      - private
    volumes:
      - ./db:/data/db

  pritunl:
    image: goofball222/pritunl:latest
    container_name: pritunl
    hostname: pritunl
    privileged: true
    sysctls:
      - net.ipv6.conf.all.disable_ipv6=0
    networks:
      - private
      - proxy
    links:
      - mongo
    volumes:
      - /etc/localtime:/etc/localtime:ro
    ports:
      - 1194:1194
      - 1194:1194/udp
    expose:
      - 9700
    environment:
      - TZ=UTC
      - MONGODB_URI=mongodb://mongo:27017/pritunl
      - REVERSE_PROXY=true
    labels:
      - traefik.backend=pritunl
      - traefik.frontend.rule=Host:<HOSTNAME>
      - traefik.port=9700
      - traefik.docker.network=proxy
      - traefik.enable=true

networks:
  proxy:
    external:
      name: proxy
  private:
    driver: bridge
    internal: true

```

---

**Environment variables:**

| Variable | Default | Description |
| :--- | :---: | --- |
| `DEBUG` | ***false*** | Set to *true* for extra entrypoint script verbosity for debugging |
| `MONGODB_URI` | ***mongodb://mongo:27017/pritunl*** | Sets the URI Pritunl will access for the Mongo DB instance |
| `REVERSE_PROXY` | ***false*** | Set to *true* to set the pritunl web interface to run in reverse-proxy mode (Traefik/nginx) |
| `PRITUNL_OPTS` | ***unset*** | Any additional custom run options for the container pritunl process

[//]: # (Licensed under the Apache 2.0 license)
[//]: # (Copyright 2018 The Goofball - goofball222@gmail.com)
