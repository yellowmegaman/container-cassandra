# container-cassandra [![Build Status](https://cloud.drone.io/api/badges/yellowmegaman/container-cassandra/status.svg)](https://cloud.drone.io/yellowmegaman/container-cassandra)

Openjdk docker image with Apache Cassandra

Nobody cares about some crazy old-school bash functions to determine private ip address. Here is an image which supports any cassandra config substitution from env variables.
Add config via volume, set $CONFIG_TEMPLATE_LOCATION and any variables you want.

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

If you set $CHMOD to "true", entrypoint will create and chown/chmod directories from those variables: 
- `$CASSANDRA_DATA_DIR`
- `$CASSANDRA_COMMITLOG_DIR` 
- `$CASSANDRA_SAVED_CACHES_DIR`

Example:

```console
docker run -v $PWD/cassandra.yaml:/opt/cassandra.yaml                  \
	   -e "CONFIG_TEMPLATE_LOCATION=/opt/cassandra.yaml"           \
	   -e "CASSANDRA_CLUSTER_NAME=github"                          \
	   -e "CASSANDRA_DATA_DIR=/opt/cassandra/data"                 \
	   -e "CASSANDRA_COMMITLOG_DIR=/opt/cassandra/commitlog"       \
	   -e "CASSANDRA_SAVED_CACHES_DIR=/opt/cassandra/saved_caches" \
	   -e "CASSANDRA_SEED_NODE=127.0.0.1"                          \
	   -e "CASSANDRA_LISTEN_ADDRESS=127.0.0.1"                     \
	   -e "CASSANDRA_START_RPC=true"                               \
	   -e "CASSANDRA_RPC_ADDRESS=localhost"                        \
	   -e "CHMOD=true" yellowmegaman/container-cassandra:latest
```

```console
# nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address    Load       Tokens       Owns (effective)  Host ID                               Rack
UN  127.0.0.1  103.73 KiB  256          100.0%            8ac7a384-131b-45a3-969c-0de86fc017f7  rack1
```
