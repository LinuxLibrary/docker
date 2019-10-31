# Overlay networks using Weave

- *Features*
	- It does not require a key-value store
	- Works with Swarm IPAM and DNS discovery but can provide its own without swarm
	- Mesh works across hosts locally, in the cloud or both
	- High performance, peer-to-peer encryption
	- Allows full UDP multicast across the network even if the underlying network does not support or allow
	- Weave Net can route through multiple hops in your cluster

- Weave Net works on the following ports
	- TCP - 6783
	- UDP - 6783, 6784

- Install weave net plugin

	```
	# docker plugin install store/weaveworks/net-plugin:latest_release
	```

- 