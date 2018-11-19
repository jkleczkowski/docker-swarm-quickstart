# [Portainer](https://portainer.io) installation guide at docker swarm

> requirements: [Swarm installed](./swarm.md)

1. At swarm manager go to `/docker` dir 
   ```sh
   cd /docker
   ```
1. Download prepaired yaml file 
   ```sh
   sudo curl -L https://jkleczkowski.github.io/docker-swarm-quickstart/swarm/portainer-swarm-stack.yml -o portainer-agent-stack.yml
   ```
1. deploy stack
   ```sh
   docker stack deploy --compose-file=portainer-swarm-stack.yml portainer
   ```
1. List services to check if two new services was added.
   ```sh
   docker service ls
   ```
   > output:
   ```
   ID           NAME                MODE       REPLICAS IMAGE                      PORTS
   z3racf3bqbgy portainer_agent     global     3/3      portainer/agent:latest
   csgf0qo0n5g4 portainer_portainer replicated 1/1      portainer/portainer:latest *:9000->9000/tcp

   ```
1. You can check effect by browsing http://YOUR_MASTER_IP:9000/ 
    > system will ask You to create admin account
 
> [Readme](../README.md)