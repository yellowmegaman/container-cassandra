# container-cassandra [![Build Status](https://cloud.drone.io/api/badges/yellowmegaman/container-cassandra/status.svg)](https://cloud.drone.io/yellowmegaman/container-cassandra)

Openjdk docker image with Apache Cassandra

Nobody cares about some crazy old-school bash functions to determine private ip address. Here is an image which supports any cassandra config substitution from env variables.
Add config via volume, set $CONFIG_TEMPLATE_LOCATION and any variables you want.

Example:
```
listen_address: $LISTEN
```

```
docker run -d -v $PWD/mycassandra.yaml:/opt/cassandra.yaml -e "CONFIG_TEMPLATE_LOCATION=/opt/cassandra.yaml" -e "LISTEN=1.2.3.4" yellowmegaman/container-cassandra:latest



```
docker pull yellowmegaman/container-cassandra:latest
docker pull quay.io/yellowmegaman/container-cassandra:latest
```
