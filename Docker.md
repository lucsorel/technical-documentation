# Docker
## Installation
From the [Docker installation guide for Ubuntu](https://docs.docker.com/engine/installation/ubuntulinux/).

```bash
# checks the Kernel version (must be >3.1.0)
uname -r

# adds the gpg key of the Docker releases repository
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

# gets Ubuntu version
lsb_release -a

# adds the repository for the distribution
sudo nano /etc/apt/sources.list.d/docker.list

deb https://apt.dockerproject.org/repo ubuntu-wily main

# updates the repository update policy
sudo apt-get update
sudo apt-get purge lxc-docker
sudo apt-cache policy docker-engine

# installs the linux-image-extra package to enable the use of the aufs storage driver
sudo apt-get install linux-image-extra-$(uname -r) # remove the trailing '-lowlatency'

# installs Docker
sudo apt-get install docker-engine

# runs Docker and checks its version
sudo service docker start
docker -v
```

## Tuning
I followed this 
[How do I change the Docker image installation directory?](https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169) blog post to "change Docker's storage base directory (where container and images go)". The `-g` option in `/etc/default/docker` did not work but the symbolinc link did:
```bash
# stops docker
sudo service docker stop

# backs docker images up
sudo tar -zcC /var/lib docker > ~/var_lib_docker-backup-$(date +%s).tar.gz

# moves the /var/lib/docker directory content to your new partition (the trailing /docker directory will be created)
sudo mv /var/lib/docker /my/folder/for

# create a symbolic link (/!\ don't use ntfs partitions, docker would freeze your system)
sudo ln -s /my/folder/for/docker /var/lib/docker

# restarts docker
sudo service docker start
```
## Docker compose
* installation (requires superuser rights, docker must be running)
```bash
sudo su

# to uninstall a previous version
rm /usr/local/bin/docker-compose

# starts docker
service docker start

# from https://docs.docker.com/compose/install/ and https://github.com/docker/compose/releases/tag/1.6.0:
curl -L https://github.com/docker/compose/releases/download/1.6.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
# test docker compose version
docker-compose -v
```

## Documentation
See the [CLI commands](https://docs.docker.com/engine/reference/commandline/cli/).

Docker flags:
* of the [run command](https://docs.docker.com/engine/reference/commandline/run/) (see the [run reference](https://docs.docker.com/engine/reference/run/))
  * -d: run a container in the detached mode/as a deamon
  * -P / -p[host port]:[container port]: map any required network ports inside the container to its host (this lets us view our web application, for example)
* delete all stopped containers with the [rm command](https://docs.docker.com/engine/reference/commandline/rm/)
```bash
docker rm $(docker ps -a -q)
```
* deletes dangling images
```bash
docker rmi $(docker images -f 'dangling=true' -q)
```
