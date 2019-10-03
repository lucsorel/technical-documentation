# Installation
* SBT from [SBT documentation](http://www.scala-sbt.org/0.13/docs/Installing-sbt-on-Linux.html):

```bash
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
sudo apt-get update
sudo apt-get install sbt
```