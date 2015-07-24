---
tags: docker
---

## Entrypoints

Entrypoint is a concept in Docker which combined with the command define which
application gets run inside the Docker container. This article briefly explains
what the entrypoint is, and how wercker makes use of it.

## What is an entrypoint

A entrypoint will set a binary which will be executed when running a command on
a Docker container. This is slightly different from the Docker command. As the
command will be concatenated together with entrypoint. By overriding the
entrypoint it is possible to change the behaviour when running a container.

Most containers do not override the entrypoint, and will just execute the
cmd. Some container however do change the entrypoint to make it easier to work
with. For example, a "ping" container might have `/bin/env` set as the
entrypoint, and will use the cmd as the arguments for ping.

```no-highlight
docker run bvdberg/ping 8.8.8.8
```

The above will create a new container based on the `wercker/ping` image, and it
will start ping to 8.8.8.8.

Checkout the following links for more information about entrypoints.

- https://docs.docker.com/reference/builder/#entrypoint
- https://docs.docker.com/reference/run/#entrypoint-default-command-to-execute-at-runtime

## Entrypoint and wercker

Wercker, by default, will reset the entrypoint when running a box, and will use
the `cmd` to execute the pipeline. If you need to change the entrypoint, then
you can add the `entrypoint` property to a box. This works on both the main box,
and on service boxes.

```yaml
box:
  id: ubuntu
  entrypoint: /bin/bash -c
```

Wercker requires a shell for the `cmd`. By default we use `/bin/bash`. If this
is not installed, or if you wish to change this you can use the `cmd` property.

```yaml
box:
  id: ubuntu
  cmd: /bin/sh
```
