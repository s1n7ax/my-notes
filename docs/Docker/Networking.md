# Default Bridge

When containers are ran using `docker run` without specifying the network name, the **default bridge** will be used.

#### Finding default bridge

```shell
# to show all the networks
docker network ls

# in the networks, "bridge" is the default bridge
# you can get more info of the bridge
docker inspect bridge

# you can find the network interface name of the bridge as follows
docker inspect bridge | grep com.docker.network.bridge.name

# shows network interface info
ip addr show docker0
```

#### Inspect the links

```shell
# by default, there will be no links to the docker0 bridge when no containers are running
bridge link | grep docker0 # this will be empty

# when container is started, the network will be connected to the default bridge when no other network is spicified
docker run -itd --rm busybox sh

# now there will be a new interface that connects to docker0 bridge
bridge link | grep docker0
```

# User Defined Bridge

Works similar to the default bridge but containers will be linked only when the network is specified to use the user defined bridge

#### Creating a user defined bridge

```shell
# first create a network
docker network create some_nework_name

# to find the network interface name, first find the network id in the docker
docker network ls --filter 'name=some_nework_name' --format '{{.ID}}'

# network interface should be created using be 'br-' prefix
ip addr show | grep 'br-<network_id>'
```

#### Create a new network withing the network

```shell
# use the --network flag to pass the network of the container
docker run -it --rm --network test some_nework_name sh

# now a new interface should be linked to the new bridge
bridge link | grep 'br-<network_id>'
```

# Host

Host network runs a container but it's similar to running an application in the host network.

#### Run a container in the host

```shell
docker run -it --rm --network host busybox sh
```

# Macvlan ()

# Macvlan ()

# ipvlan (l2)

# ipvlan (l3)
