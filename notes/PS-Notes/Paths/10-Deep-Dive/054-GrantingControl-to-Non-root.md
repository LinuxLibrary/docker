# Granting Docker Control to Non-root

- For doing this we need to add the desired user to the docker group
- But there will be a lot of security consequencies, to avoid this...
	- Control which user accounts are members of this group
	- Regularly audit the membership of the docker group
- Adding a user to docker group

	```
	# gpasswd -a ashrinivas docker
	```

- Launch and test a container

	```
	# docker run -it ubuntu /bin/bash
	```