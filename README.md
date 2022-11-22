# Deploy Services

## Prepare the docker overlay network with swarm

```bash
$ docker swarm init   # init will tell you how to join the swarm cluster

# create the attachable overlay network for services to be discovered across host machines
$ docker network create -d overlay --attachable MY-OVERLAY-NETWORK

# on other worker nodes, join the swarm cluster:
$ docker swarm join --token TOKEN_GERNEATED_BY_SWARM_INIT
```



## Deploy OpenSearch

```bash
# Assume we got 3 nodes for opensearch node1/node2/dashboard

# On host node 1
$ docker-compose -f opensearch-node1.yml up -d

# On host node 2
$ docker-compose -f opensearch-node2.yaml up -d

# On host node 3
$ docker-compose -f opensearch-dashboard.yml up -d

# Tips:
# The compose yaml files described the overlay network's name, which should be the same with that created in the step above.
# The description of the network:
# overlay: true
# driver: overlay
# These 2 properties are the key for swarm to automatically create network for the services.

# Another point to be noticed is: make sure the opensearch cluster nodes' names should keep accordance with the compose serivces' names.
```

