# Updating Docker

- Download and add GPG Key

	```
	# wget -qO https://get.docker.com/gpg | apt-key add - 
	```

- Add docker apt repo

	```
	# echo deb http://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list
	```

- Update or sync with the new repo

	```
	# apt-get update
	```

- Install LXC-Docker

	```
	# apt-get install lxc-docker
	```
	