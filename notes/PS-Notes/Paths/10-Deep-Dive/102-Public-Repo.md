# Docker Public Repo

- Docker Hub is the default Public Registry for Docker
- Create an account at `hub.docker.com` and login to it
- Click Add repository
- Give a name and description and click on `Add Repository`
- To upload the images to this repository from your machine
	- Tag your image

	```
	# docker tag <__IMAGE-ID__> <__USER-NAME__/__NAME__:__VERSION__>

	Ex:
	# docker tag xXXxxxXX999x vmsnivas/helloworld:1.0
	```

	- Push the image to your repository

	```
	# docker push vmsnivas/helloworld:1.0
	```

	> NOTE: This will prompt for your username and password of your docker hub account

	>> This will try to push all the layers of the image is they don't exist on Docker Hub. If they does exists on docker hub then those layers will be skipped