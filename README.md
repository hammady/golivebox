# golivebox

Docker application bundle to broadcast live prayers audio streams to a SHOUTcast server.

## System Requirements
Docker running in swarm mode.
- Install [Docker 19.03+](https://docs.docker.com/engine/install/).
- Enable swarm mode (`docker swarm init`)

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
docker app run --name golivebox4 \
    --parameters-file overrides.yml \
    hammady/golivebox:latest
```

### Upgrade
