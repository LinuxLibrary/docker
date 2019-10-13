# Docker Overlay Networks

- Containers only connect to other containers on the same network
- Connecting to containers on the other hosts requires that the container publish the needed ports
- Overlay network allows containers running on different hosts to connect on a private network

- *Prerequisites*
	- Requires Docker Swarm or a key-value store
	- Supported stores: Consul, etcd, Zookeeper

- Docker overlay networks requires the following ports to be open on the host
	- 4789 - UDP used for Docker Overlay network
	- 7946 - TCP & UDP used by the Docker Swarm
		- For docker swarm we need open both the above ports

- Let us create a docker overlay network in a swarm cluster on the master node

	```
	# docker network create -d overlay --attachable=true frontend
	```

	- `-d` flag is used to mention the driver
	- `--attachable` is used to allow containers manually attach to this nerwork

- To see the docker networks

	```
	# docker network ls
	```

- Now let us try to run the busybox container in this network on all the swarm nodes

	```
	# docker container run --rm -it --network=frontend --name bb-$HOSTNAME busybox:1.27
	```

	- If we check the ip addresses on both the containers we can see those being in the same network

	```
	# ip addr
	```

	- Even we can try to ping between the containers

- By default docker will connect the overlay networks to bridged network which ensures all of the containers connected to overlay network and also access external resources