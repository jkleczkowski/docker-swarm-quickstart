# [Portainer](https://portainer.io) installation guide at docker swarm

> requirements: [Swarm installed](./swarm.md)

1. At swarm manager go to `/docker` dir 
   ```sh
   cd /docker
   ```
1. Download prepaired yaml file 
   ```sh
   sudo curl -L https://jkleczkowski.github.io/docker-swarm-quickstart/swarm/portainer-agent-stack.yml -o portainer-agent-stack.yml
   ```
1. you can check effect browsing http://YOUR_MASTER_IP:9000/ 
1. 