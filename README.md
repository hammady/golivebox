# golivebox

Docker Compose application to broadcast live prayers audio streams to a SHOUTcast/Icecast server.

## System Requirements
- Install [Docker](https://docs.docker.com/engine/install/).
- Install [Docker Compose](https://docs.docker.com/compose/install/).

## Configure

Clone this repository to your home directory, then do the following:

- Create an empty database file for filebrowser: `touch filebrowser.db`.
- Copy `example.env` to `.env` and set values for all environment variables.

## Run

Start:
```bash
docker-compose up -d
```

Monitor:
```bash
docker-compose ps
```

Follow logs:
```bash
docker-compose logs -f 
```

Stop:
```bash
docker-compose down
```
