# Docker Swarm Mode

- Swarm mode is a native clustering
- A collection of docker engines joined into a cluster is Swarm
- Docker engines which run on a node in the swarm run in Swarm Mode
- Swarm contains 1 or more Manager Nodes and 1 or more working nodes
- Manager nodes are highly available (HA)
- *Manager nodes should always be in odd numbers*
- Manager nodes looks after the state of the cluster and dispatch tasks to the working nodes
- Only one will be the leader among the Manager Nodes
- Worker nodes execute the tasks/services
- Services are declaritive and scalable
- A task is the atomic unit of work assigned to working nodes