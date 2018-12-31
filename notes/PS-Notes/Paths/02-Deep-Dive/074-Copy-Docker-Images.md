# Copying Docker Images between hosts

- If we do any modifications to the image at the runtime, means we are adding some content to the image while running a docker container using the docker image. In that case we can commit that change to the image using `docker commit`
- For example I am adding a file to the container based out of an image. I want to make these changes permanent.

	```
	# docker run ubuntu /bin/bash -c "echo 'test file' > /tmp/testfile" --name testcontainer
	```

	- Now we need to commit this change to the image

	```
	# docker commit testcontainer newtestimage
	```

	- Now we have a new image named `newtestimage`
	- Now save the new image to a tar

	```
	# docker save -o /tmp/newtestimage.tar newtestimage
	```

- Now we have the image in the tar file. All we need to do is we need to copy this tar file to our desired machine and need to load it

	- Once after copying the tar we need to load that to docker images

	```
	# docker load -i /tmp/newtestimage.tar
	```

	- Now we can see this in the docker images

	```
	# docker images
	```