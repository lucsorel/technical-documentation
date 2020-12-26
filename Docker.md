# Docker
## Installation
Two options:

* the short one 

```
wget -qO- https://get.docker.com/ | sh
```

* the official way from the [Docker installation guide for Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

```bash
# checks the Kernel version (must be >3.1.0)
uname -r

# install packages to allow apt to use a repository over HTTPS
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common gnupg-agent

# adds the gpg key of the Docker releases repository
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# gets Ubuntu version
lsb_release -cs
# but LinuxMint versions override it (Sonya -> xenial)

# adds the repository for the distribution
## (Ubuntu)
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
## (LinuxMint)
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

# updates the repository update policy
sudo apt-get update
sudo apt-get purge lxc-docker docker docker-engine docker.io
sudo apt-cache madison docker-ce

# installs Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io
 
# runs Docker and checks its version
sudo service docker start
docker -v
```

Adds the current user to the docker group (see [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/)):

```sh
sudo groupadd docker
sudo usermod -aG docker $USER
# then log out and log in again to account for the change
```

## Tuning
I followed this 
[How do I change the Docker image installation directory?](https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169) blog post to "change Docker's storage base directory (where containers and images go)". The `-g` option in `/etc/default/docker` did not work but the symbolinc link did:
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

* installation (requires superuser rights)

```bash
sudo su

# to uninstall a previous version
rm /usr/local/bin/docker-compose

# stops docker
service docker stop

# from https://docs.docker.com/compose/install/ and https://github.com/docker/compose/releases/tag/1.6.0:
curl -L https://github.com/docker/compose/releases/download/1.6.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

# makes the docker-compose binary executable
chmod +x /usr/local/bin/docker-compose

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

* forces the deletion of all images
```bash
docker rmi -f $(docker images -q)
```
