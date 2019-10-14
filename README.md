# My COMMENTS
### Swarm Node setup: 

```docker run -v /tmp/hostdata:/data -d --rm -e DATADIR=/data -e PASSWORD=password123 -p 8501:8500/tcp -it --name swarm1 ethdevops/swarm --httpaddr=0.0.0.0 --debug --verbosity 4 --datadir /data```

```curl -X POST -H "Content-Type: text/plain" --data "some-data" http://52.8.30.100:8501/bzz:/```


### upload a file:
```curl -H "Content-Type: text/html" --data-binary @website/ICO_only.html http://52.8.30.100:8501/bzz:/ ```
# Official Swarm Docker image

[![Build Status](https://travis-ci.org/ethersphere/swarm-docker.svg?branch=master)](https://travis-ci.org/ethersphere/swarm-docker)

`Dockerfile` for `swarm` used on https://swarm-gateways.net and https://open.swarm-gateways.net

## Docker tags

* `latest` - latest stable release
* `edge` - latest build from `master`
* `v0.x.y` - specific stable release

## Environment variables

* `PASSWORD` - *required* - Used to setup a sample Ethereum account in the data directory. If a data directory is mounted with a volume, the first Ethereum account from it is loaded, and Swarm will try to decrypt it non-interactively with `PASSWORD`
* `DATADIR` - *optional* - Defaults to `/root/.ethereum`
* `CONTAINER_NAME` - *optional* - Defaults to `localhost`, used as a prefix for measurements and log lines

## Swarm command line arguments

All Swarm command line arguments are supported and can be sent as part of the CMD field to the Docker container

## Pulling the image

    $ docker pull ethdevops/swarm:latest

## Running a Swarm container from the command line

    $ docker run -e PASSWORD=password123 -t ethdevops/swarm:latest \
                              --debug \
                              --verbosity 4

## Running a Swarm container with custom ENS endpoint

    $ docker run -e PASSWORD=password123 -t ethdevops/swarm:latest \
                              --ens-api http://1.2.3.4:8545 \
                              --debug \
                              --verbosity 4

## Running a Swarm container with metrics enabled

    $ docker run -e PASSWORD=password123 -t ethdevops/swarm:latest \
                              --debug \
                              --metrics \
                              --metrics.influxdb.export \
                              --metrics.influxdb.endpoint "http://localhost:8086" \
                              --metrics.influxdb.username "user" \
                              --metrics.influxdb.password "pass" \
                              --metrics.influxdb.database "metrics" \
                              --metrics.influxdb.host.tag "localhost" \
                              --verbosity 4

## Running a Swarm container with tracing and pprof server enabled

    $ docker run -e PASSWORD=password123 -t ethdevops/swarm:latest \
                              --debug \
                              --tracing \
                              --tracing.endpoint 127.0.0.1:6831 \
                              --tracing.svc myswarm \
                              --pprof \
                              --pprofaddr 0.0.0.0 \
                              --pprofport 6060

## Running a Swarm container with custom data directory mounted from a volume

    $ docker run -e DATADIR=/data -e PASSWORD=password123 -v /tmp/hostdata:/data -t ethdevops/swarm:latest \
                              --debug \
                              --verbosity 4
