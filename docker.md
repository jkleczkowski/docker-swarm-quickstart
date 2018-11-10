# docker installation

1. Install updates and docker at all nodes
   ```sh
   sudo apt update && sudo apt upgrade -y && sudo apt install -y docker.io 
   ```
1. Add current user to docker group 
   ```sh 
   sudo usermod -aG docker $USER
   ```
1. Prepare `DOCKER_VOL`, in this scenario we will use `/docker/volumes` dir for persistent storage directory.
   ```sh 
   sudo mkdir /docker
   sudo chown :docker /docker
   sudo mkdir /docker/volumes
   #add to env
   sudo bash -c 'echo DOCKER_VOL=/docker/volumes >> /etc/environment'
   export DOCKER_VOL=/docker/volumes
   ```

   ---
> [Readme](./README.md)
