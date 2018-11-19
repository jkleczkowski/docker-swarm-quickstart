# Docker swarm installation guide
___

> **Prefered base server for me is Ubuntu 18.xx**

> requirements: [Installed docker](../docker.md)

1. Prepare at least 2 machines
    - master
    - node
1. Install updates and docker at all nodes
   ```sh
   sudo apt update && sudo apt upgrade -y && sudo apt install -y docker.io 
   ```
1. Add current user to docker group 
   ```sh 
   sudo usermod -aG docker $USER
   ```
1. At manager machine initialize **swarm**
   ```sh
   docker swarm init
   ```
   
   > output should look like:
   
   ```
   Swarm initialized: current node (1g4sfirk42j2r0y50w9bgrrzt) is now a manager.
   To add a worker to this swarm, run the following command:
   
   docker swarm join --token SWMTKN-1-1fheqo561pf7rdx4csaxwrcso7yme71gr0o5oadus21y3hqerq-78ma3s72n53uq2gkbvjriyxso 10.0.0.4:2377
   
   To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
   ```
1. At every node machine run command from manager output.
1. Another important thing is that sometimes after host restart nodes do not connect to manager. To prevent this behavior we can use simple trick by adding `docker ps` command to cron and restart cron service
   ```sh
   sudo bash -c 'echo "* *     * * *   root    docker ps -a > /tmp/docker.state.txt" >> /etc/crontab'
   sudo service cron restart
   ```
1. From now we have swarm initialized check that all nodes are connected
    ```sh
    docker node ls
    ```
    > output should look like:
    ```
    ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
    1g4sfirk42j2r0y50w9bgrrzt *   vt-master           Ready               Active              Leader              18.06.1-ce
    m1umwdcbvghk43lbewzzmgsix     vt-node-1           Ready               Active                                  18.06.1-ce
    b0gw2m44msjla5bdso0gil0pj     vt-node-2           Ready               Active                                  18.06.1-ce
    ```
1. create `core-infra` network for comunicating with other containers
   ```sh
   docker network create core-infra --attachable -d overlay --subnet 10.4.0.0/16 --ip-range 10.4.0.0/16 --gateway 10.4.0.1
   ```
---
> [Readme](../README.md)

> [Install Portainer](./portainer.md)
