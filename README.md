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

## Optional cassandra.yaml, not baked-in.

Example cassandra.yaml contains the following env vars:
```
cluster_name: '$CASSANDRA_CLUSTER_NAME'
$CASSANDRA_DATA_DIR
commitlog_directory: $CASSANDRA_COMMITLOG_DIR
saved_caches_directory: $CASSANDRA_SAVED_CACHES_DIR
seeds: "$CASSANDRA_SEED_NODE"
listen_address: $CASSANDRA_LISTEN_ADDRESS
start_rpc: $CASSANDRA_START_RPC
rpc_address: $CASSANDRA_RPC_ADDRESS
```

If you set $CHMOD to "true, entrypoint will chown/chmod $CASSANDRA_DATA_DIR $CASSANDRA_COMMITLOG_DIR $CASSANDRA_SAVED_CACHES_DIR directories.
