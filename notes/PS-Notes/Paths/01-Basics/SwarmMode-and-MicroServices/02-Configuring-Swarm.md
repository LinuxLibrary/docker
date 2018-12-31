# Configuring Swarm Mode

- To configure we require Docker 1.12 or later
- Let us configure 3 manager nodes and 3 worker nodes
- Let us first configure the `mgr01` node which is one of our 3 manager nodes and ready with the pre-requisites configured
- Let us initialize the docker swarm mode

```
# docker swarm init --advertize-addr 172.31.12.161:2377 --listen-addr 172.31.12.161:2377
```

> NOTE: `--advertize-addr` is what the swarm works on. For swarm related stuff we need to use the address specified by this. `--listen-addr` is which the nodes listen the swarm traffic on the swarm manager.

- Let us know about some ports we use here
	- Engine Port		: 2375
	- Secure Engine Port	: 2376
	- Swarm Port		: 2377

- Now the above command will initialize swarm and will give us a token which can be used to manage things on this swarm
- To add another manager to this swarm 

	```
	# docker swarm join-token manager
	```

	- This will show the complete command along with the token that can be used to add a manager

- To add a worker to this swarm 

	```
	# docker swarm join-token worker
	```

	- This will show the complete command along with the token that can be used to add a worker

- Let us see how to add another manager
	- We need to get the token from the first manager node and run it on the second manager node

	```
	(mgr01)# docker swarm join-token manager # Run this on mgr01
	(mgr02)# docker swarm join --token SWMTKN-1-XXXXXXXXXXXXXXXXXXXXXXXXXXX-aaaaaaa 172.31.12.161:2377 --advertise-addr 172.31.12.162:2377 --listen-addr 172.31.12.162:2377
	```
	
	- Here we are using the address of the second node as the `advertise-addr` and `listen-addr`
- Let us add the third manager node

	```
	(mgr01)# docker swarm join-token manager # Run this on mgr01
	(mgr03)# docker swarm join --token SWMTKN-1-XXXXXXXXXXXXXXXXXXXXXXXXXXX-aaaaaaaa 172.31.12.161:2377 --advertise-addr 172.31.12.163:2377 --listen-addr 172.31.12.163:2377
	```

- We can know the complete information of the swarm as well as the node which we are on

	```
	# docker node ls
	```

	- This will display the information of all the nodes also the status of the nodes like which one of these is the master.
	- The `*` symbol between the ID and the HOSTNAME tells us the host which we are currently logged on
- In the meanwhile if we want to make any of the worker node as a manager then we can do it in the following way

	```
	# docker node promote <ID>
	```

- Adding the workers:
	- For adding the worker also we need to get the token first from the main manager node which is `mgr01` in our case

	```
	(mgr01)# docker swarm join-token worker
	(worker01) # docker swarm join --token SWMTKN-1-XXXXXXXXXXXXXXXXXXXXXXXXXXX-bbbbbbbb 172.31.12.161:2377 --advertise-addr 172.31.16.164:2377 --listen-addr 172.31.12.164:2377
	(worker02) # docker swarm join --token SWMTKN-1-XXXXXXXXXXXXXXXXXXXXXXXXXXX-bbbbbbbb 172.31.12.161:2377 --advertise-addr 172.31.16.165:2377 --listen-addr 172.31.12.165:2377
	(worker03) # docker swarm join --token SWMTKN-1-XXXXXXXXXXXXXXXXXXXXXXXXXXX-bbbbbbbb 172.31.12.161:2377 --advertise-addr 172.31.16.166:2377 --listen-addr 172.31.12.166:2377
	```

- Now let us check the details of the swarm from `mgr01`

	```
	(mgr01)# docker node ls
	```

	- From the output we can notice the `MANAGER STATUS` column being empty for the 3 worker nodes
	- This information can be available from `docker info` as well. There we can see the details of the swarm.