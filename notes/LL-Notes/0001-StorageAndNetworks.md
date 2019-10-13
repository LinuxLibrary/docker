# Storage and Networks

- Shared Storage
	- Why shared storage
		- Running services usually need data
		- Examples: NFS, iSCSI, Amazon Elastic Block Store, GCE Persistent Disk, Gluster, Ceph RBD, OpenStack Cinder
		- Allows for Container mobility
		- Choose what fits your needs
		- Docker lets you mix and match storage providers

- Let us work with the Rex Ray driver from DELL
- Download and install RexRay driver

	```
	# curl -sSL https://dl.bintray.com/emccode/rexray/install | sudo sh -
	```

- To use the storage provider we need to create the following config

	```
	libstorage:
	  service: rbd
	  server:
	    services:
	      rbd:
	        driver: rbd
	        rbd:
	          defaultPool: rbd
	```

- Start the service

	```
	# rexray service start
	```

- Install the docker plugin

	```
	# docker plugin install rexray/rbd RBD_DEFAULTPOOL=rbd
	```

- Create a new volume

	```
	# docker volume create --driver=rexray/rbd -o size=20 --name test
	```

	- Here `--driver=rexray/rbd` creates an rbd image in the rex cluster 
	- `-o` option will allow us to give additional optionals to the driver
	- Size we are providing in GBs
	- `--name` allows us to give a name to the volume

- Show the volumes

	```
	# docker volume ls
	```

	- To get the details of the volume

	```
	# docker volume inspect <VOLUME_NAME>
	```

- Mount a volume

	```
	# docker container run -it --mount source=test,dst=/test --name bb busybox:1.27
	```

	- `--mount` option is used to mount a volume on to the container
	- `source` is used to specify the source volume name
	- `dst` is used to specify the destination mount point in the container

- Remove volume

	```
	# docker volume rm <VOLUME_NAME>
	```

	- Volume can not be removed if it is mounted on to a container even if it is not running.