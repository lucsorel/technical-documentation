# Docker
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
