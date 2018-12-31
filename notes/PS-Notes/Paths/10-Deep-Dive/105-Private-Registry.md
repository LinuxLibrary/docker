# Working with Docker Private Registry

- We can get a ready to use private registry image from docker
- Pull the docker registry image

	```
	# docker run -d -p 5000:5000 registry
	```

- Now choose an image and push it to your private registry
	- Tag that instance with the following format
	- docker tag <__IMAGE-ID__> <__DOCKER_REGISTRY_HOST_IP__>:<__REGISTRY_PORT__>/<__REPO_NAME__>

	```
	# docker tag xXXxXX9X9999 192.168.10.101:5000/helloworld
	# docker push 192.168.10.101:5000/helloworld
	```

	- Before doing this we need to change the Docker Options to choose the default docker registry
	- On UBUNTU, edit /etc/default/docker

	```
	DOCKER_OPTS="--insecure-registry 192.168.10.101:5000"
	```

	- On CentOS edit 