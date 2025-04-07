# Docker image of PostgreSQL with vector database extension **pgvector** on Alpine Linux

<style type="text/css" media="screen">
.success{padding:1rem;border-radius:0.5em;background-color:#95d5b2;color:black}
.warn{padding:1rem;border-radius:0.5em;background-color:#ffe1a8;color:#250902}
.success a:link { color:#33348e; text-decoration: none; }
.success a:visited { color:#33348e; text-decoration: none; }
.success a:hover { color:#33348e; text-decoration: none; }
.success a:active { color:#7476b4; text-decoration: underline; }
</style>

## Goals

- To build a Docker image which makes a small image-size footprint.
- To make quick installable **docker compose** services, which support both relational and vector databases.

## Versions used

| **Alpine**     | 3.21  |
|----------------|-------|
| **PostgreSQL** | 15.12 |
| **Pgvector**   | 0.8.0 |

## Requrements

Docker version >= **version 23.0**,  in which Docker **BuildKit** was introduced. To check this issue enter a terminal command:

```shell
docker buildx build --help
```

Probably, an older Docker version would be work. But this is not garanteed. See [Creating Issues](#creating-issues)

---

## Create/build an image locally  using cloning this repo workflow

### 1. Clone the repo

### 2. Build the image with Docker CLI

#### Command:  docker build [OPTIONS] PATH | URL | -

#### Argument Descripton

The last parameter **PATH | URL | -**  is called a  [Build Context](https://docs.docker.com/build/concepts/context/)
In case of default repo clone, PATH is relative path, which points to current directory.

#### OPTIONS Description

| **OPTION**     | Description                                   |
|----------------|-----------------------------------------------|
|**-t**          | Name and optionally a tag (format: "name:tag")|
|**-D, --debug** | Enable debug logging                          |
| **--no-cache** | Do not use cache when building the image      |
|**--build-arg** | Set build-time variables                      |

#### Example:(assumes you clone the repo in the directory by default)

```shell
cd ./docker_alpine-pg-pgvector
docker build -t zigr/pg15-pgvector08:alpine3.21 [--build-arg=""] [-D] [--no-cache] .
```

**See** [⚠️ Notice below](#important-note)

---

<div class="success">

## 😎 More quick way. Create/build an image from remote github repository

### Example

```shell
docker build -t zigr/pg15-pgvector08:alpine3.21 [--build-arg=""] [-D] [--no-cache] https://github.com/Zigr/docker_alpine-pg-pgvector.git#master:Dockerfile

```

**See** [⚠️ Notice below](#important-note)

</div>

---

## Create and run a new container from an image

### Command:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

### Argument Descripton

|**ARGUMENT** | Description                       |
|-------------|-----------------------------------|
|**IMAGE**    | The only required command argument|

### OPTIONS Description

|**OPTION**       | Description                                 |
|-----------------|---------------------------------------------|
|**--name**        | Assign a name to the container             |
|**-p, --publish** | Publish a container's port(s) to the host  |
|**--mount**       | Attach a file system mount to the container|
|**-e, --env**     | Set environment variables                  |

#### Example

```shell
docker run --name my_pg_pgvector -p 5432:5432 --mount type=volume,src=my_pg_data,dst=/var/lib/postgresql/data,volume-nocopy -e POSTGRES_DB=mydb -e POSTGRES_USER=root -e POSTGRES_PASSWORD=!ChangeMe! -e PGDATA=/var/lib/postgresql/data/pgdata zigr/pg15-pgvector08:alpine3.21
```

**See** [⚠️ Notice below](#important-note)

---
<div class="warn" >

## Important Note

- remove brackets around OPTION(s), i.e. [OPTION] -> OPTION  in order the OPTION will take effect
- or replace [OPTION] with a space character, i.e [OPTION] -> <space character> in order the  [OPTION] will not be present in a command

</div>

---

## Creating Issues

In case of image does not build or/and run, then  <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-an-issue" target="_blank" >create an issue</a>.
