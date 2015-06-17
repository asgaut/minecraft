# Minecraft server in a docker container

To use with Ubuntu server 14.04 LTS

Install docker:

    sudo apt-get update ; sudo apt-get install lxc-docker

## Building the docker image
    git clone https://github.com/asgaut/minecraft
    cd minecraft
    sudo docker build -t minecraft-image .

## Running in container
Create dir for static storage:

    sudo mkdir -p /mnt/minecraft

Run interactive (access the Minecraft server shell):

    sudo docker run -it -p=25565:25565 -p=25565:25565/udp -v=/mnt/minecraft:/data minecraft-image

In interactive mode you can add your Minecraft user to "operators" (which is the server administrators)
with "/op username". This adds the user to 
/mnt/minecraft/ops.json (Note: connect to the server with the Minecraft client before running /op command)
Exit interactive mode (and server process) with "/stop".

Run as daemon

    sudo docker run -d=true -p=25565:25565/tcp -p=25565:25565/udp -v=/mnt/minecraft:/data minecraft-image
