# golivebox

Docker application bundle to broadcast live prayers audio streams to a SHOUTcast server.

## System Requirements
Docker running in swarm mode, and BUTT running as a separate (privileged) container.
- Install [Docker 19.03+](https://docs.docker.com/engine/install/).
- Enable swarm mode (`docker swarm init`)
- Run [BUTT](https://github.com/hammady/butt-docker) as a separate container with access to host devices.
This container cannot run using swarm mode which does not support privileged mode or devices.
Make sure to use a production image (e.g. `ghcr.io/hammady/butt-docker:0.1.34`) when running in production. To serve recordings, make sure you mount `/data` to the same host path defined
below in filebrowser (`/path/to/webroot`).
- Create an empty database file for filebrowser: `touch /path/to/filebrowser.db`

## Development

### Configure

- Edit `golivebox.dockerapp/parameters.yml` to set default values for all parameters.
- Edit `golivebox.dockerapp/docker-compose.yml` to configure all services.
- Edit `golivebox.dockerapp/metadata.yml` to set name, description and version.

### Build
    
```bash
docker app build -t hammady/golivebox:latest golivebox.dockerapp
```

### Run

```bash
docker app run --name golivebox1 hammady/golivebox:latest
```

### Push

```bash
docker app push hammady/golivebox:latest
```

TODO: configure a GitHub action to automatically build and push the image.

## Production

### Configure

Create a file (e.g. `overrides.yml`) to override default parameters and use it in the run command.
This file should have the same schema of the `parameters.yml` file.
You do not have to override all parameters.

### Install

```bash
docker app run --name golivebox1 \
    --set filebrowser.user=$(id -u):$(id -g) \
    --set filebrowser.server_path=/path/to/webroot \
    --set filebrowser.database_path=/path/to/filebrowser.db \
    --parameters-file overrides.yml \
    hammady/golivebox:latest
```

### Update

```bash
docker app update \
    --set key=updated_value \
    --parameters-file updated_overrides.yml \
    golivebox1
```
