
---
date: 2016-07-13
title: "Data Dog & Docker Cloud"
slug: "datadog-and-docker-cloud"
tags: [ "cloud", "docker" ]
categories: [ "development" ]
---

The configuration you need to get up and runing with Docker Cloud and Datadog.

_Don't forget to set your `API_KEY`_

```yaml
datadog:
  image: 'datadog/docker-dd-agent:latest'
  autoredeploy: true
  deployment_strategy: every_node
  environment:
    - HOSTNAME=$DOCKERCLOUD_NODE_HOSTNAME
    - API_KEY=XXX
  privileged: true
  restart: always
  tags:
    - production
  volumes:
    - '/var/run/docker.sock:/var/run/docker.sock'
    - '/proc/:/host/proc/:ro'
    - '/sys/fs/cgroup/:/host/sys/fs/cgroup:ro'
```
