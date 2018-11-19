# Gateway consul / registrator / fabio installation guide at docker swarm

> requirements: [Swarm installed](./swarm.md) 

> optional [portainer](./portainer.md)

In this step we will deploy gateway stack 
    
- [consul](https://consul.io) - as our service discovery 
- [registrator](http://gliderlabs.github.io/registrator/) - for automatic service register
- [fabio](https://fabiolb.net/) - as our gateway
  


1. At swarm manager go to `/docker` dir 
   ```sh
   cd /docker
   sudo mkdir ${DOCKER_VOL}/consul
   sudo mkdir ${DOCKER_VOL}/consul/data
   sudo mkdir ${DOCKER_VOL}/fabio
   ```
1. download consul config template
   ```sh 
   sudo curl -L https://jkleczkowski.github.io/docker-swarm-quickstart/swarm/consul-config.json -o ${DOCKER_VOL}/consul/config.json
   ```
1. download fabio config template
   ```sh 
   sudo curl -L https://jkleczkowski.github.io/docker-swarm-quickstart/swarm/fabio.properties -o ${DOCKER_VOL}/fabio/fabio.properties
   ```
   > note: I've changed default (9998) port to 80 and (9999) to 10000 
1. Prepare new network `core-infra` `docker network new core-infra`
1. Download prepaired yaml file 
   ```sh
   sudo curl -L https://jkleczkowski.github.io/docker-swarm-quickstart/swarm/gateway-swarm-stack.yml -o gateway-swarm-stack.yml
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
5. You can check effect by browsing http://YOUR_MASTER_IP:9000/ 
    > system will ask You to create admin account
 
> [Readme](../README.md)