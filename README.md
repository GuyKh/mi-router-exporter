# mi-router-exporter

Reads Mi Router data from the API and exports it in a Prometheus format.

## How does it work?
- It fetches the data from the Mi Router API ...
- ... parses it ...
- ... and exposes it in a format that Prometheus can consume.

## How to run it?
To run the container (for configuration, see below):

```
docker run -it \
    -d --name=mi-router-exporter \
    -e PASSWORD=<insert your admin password here> \
    -p 3030:3030 \
    --restart unless-stopped \
    mi-router-exporter
```

or use `docker-compose` syntax:
```
services:
  mi-router-exporter:
    image: guykhmel/mi-router-exporter
    container_name: mi-router-exporter
    restart: unless-stopped
    ports:
      - "3030:3030"
    environment:
      - PASSWORD=<Password>
      #- URL=192.168.2.1 -- # OPTIONAL - Default: 192.168.2.1
```

4. Open `http://localhost:3030/metrics` in browser, it should display metrics.
5. If there were errors, check out the container logs.

## Build
1. Clone this repo
2. Enter the folder - `cd mi-router-exporter`
3. Build the container:

```
docker build -t mi-router-exporter .
```

3. Run the container (for configuration, see below):

```
docker run -it \
    -d --name=mi-router-exporter \
    -e PASSWORD=<insert your admin password here> \
    -p 3030:3030 \
    --restart unless-stopped \
    mi-router-exporter
```

## Configration

All the configuration is done through the environmental variables.
- `LOG_LEVEL` - integration logging level. Default: `warn`. If something isn't working, try setting it to `debug` and check what's inside.
- `PASSWORD` - Mi Router admin URL. Will throw an exception if this is not set.
- `URL` - Mi Router admin IP. Default is 192.168.31.1

# Grafana integration

Check `grafana-dashboard.json` for JSON dashboard file to be consumed by Grafana.
