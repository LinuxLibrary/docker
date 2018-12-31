# Docker Communication

- Docker listens locally. But we can make that to listen on network as well.
- For this if we have multiple machines running docker, then we need to host a docker server among those.
- Below are the steps of doing that.
	- Stop the docker daemon

	```
	# service docker stop
	```

	- Start docker over Non-SSL tcp port (2375) in daemon mode

	```
	# docker -H <__IP_ADDRESS__>:<__PORT__> -d &
	```

	- On the other machine we need to configure the DOCKER_HOST with the above details of the server

	```
	# export DOCKER_HOST="tcp://<__IP_ADDRESS__>:<__PORT__>"
	```

	- If we are doing in the above way anyone can run the containers as it is not bound with the docker socket.
	- In the local method root/members of docker group only can communicate to docker as only those people can access the docker socket
	- If we want to secure the docker in this mode as well the we need to start docker with network port and socket as well

	```
	# docker -H <__IP_ADDRESS__>:<__PORT__> -H unix:///var/run/docker.sock -d &
	```