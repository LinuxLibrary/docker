# Services

- Services are declarative
- Below is the format of the `docker service`

```
Syntax: docker service < create | ls | ps | inspect | update | rm >
# docker service create --name <SERVICE_NAME> -p <SRC_PORT>:<DEST_PORT> --replicas <NO_OF_INSTANCES> <DOCKER_IMAGE>

Ex:
# docker service create --name psight -p 8080:8080 --replicas 5 nigelpoulton/pluralsight-docker-ci
```

- Now we can check that using `docker service ls`
- We can also check the details of the processes, on which node those are and their status

```
# docker service ps psight
```

- In the above case we have 5 docker containers running for the service `psight`
- Some times depending on the load we need more containers working for the service. In such case we need to scale up some more instances
- We have 2 ways of doing that
	- Through `docker service scale`

	```
	Syntax: docker service scale <SERVICE_NAME>=<NO_OF_INSTANCES>

	# docker service scale psight=10
	```

	- Through `docker service update`

	```
	Syntax: docker service update --replicas <NO_OF_INSTANCES> <SERVICE_NAME>

	# docker service update --replicas 10 psight
	```

- If in somecase any of the above manager or worker nodes went down accidentally due to power issues or anything else they can be picked up automatically into the pool once they are available.
- But that host won't get any of the existing tasks onto it until we scale the service with more number of instances/replicas. Means it does not rebalance any existance tasks and only can pick up the new tasks.