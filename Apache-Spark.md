# Setup
## Python
```bash
# displays the available versions of Python
apt-cache search python | egrep "^python[0-9].[0-9] " --color

# install Python
sudo apt-get install python

# check Python version
python --version
```

### IDE
### Stani Python Editor
```bash
sudo apt-get install spe
```

### Atom, configuration, modules
Use a [PPA](http://www.webupd8.org/2014/06/atom-text-editor-available-for-linux.html) to install the most up-to-date version:
```bash
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```

* install [git-control](https://atom.io/packages/git-control) to retrieve and push code editions to the central repository
* [markdown-preview](https://atom.io/packages/markdown-preview) is usually already installed
* uninstall/disable `language-c`, `language-csharp` (many more could be disabled) for speed improvement, `metrics` to disable the Google Analytics tracking of Atom use

Settings:
* `Settings` section:
  * Show Line Numbers
  * Soft Tabs
  * Font Size: 15 (suggestion)
  * Tab Length: 4
* make sure that the `Ensure Single Trailing Newline` checkbox of the `whitespace` package is checked to make Atom add a newline character at the end of edited files

## Java JDK
Install Oracle Java JDK8 [via PPA](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html):
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer

sudo update-java-alternatives -s java-8-oracle

# check Java version
java -version
```

## Apache Spark
* [download page](http://spark.apache.org/downloads.html): latest Spark release (`1.5.2`) with the latest pre-built for Hadoop (`2.6 and later`)

```bash
# given MD5 sum:
spark-1.5.2-bin-hadoop2.6.tgz: 0A 09 0C 5E BF 72 54 D9  B3 29 51 C8 56 FA 92 FA

# tested MD5 sum:
md5sum spark-1.5.2-bin-hadoop2.6.tgz
0a090c5ebf7254d9b32951c856fa92fa  spark-1.5.2-bin-hadoop2.6.tgz
```

* unzipped and renamed the extracted folder to `[mooc folder]/spark`

* changed the Spark default configuration to reduce the logs noise
```bash
# spark/conf/log4j.properties.template -> log4j.properties
#log4j.rootCategory=INFO, console
log4j.rootCategory=WARN, console
```

* define a system variable to tell where spark is installed
```bash
# defines the system variable temporarily
export SPARK_HOME=/home/luc/devbox/MooC/Taming-big-data-with-Apache-Spark/spark

# updates the PATH
PATH=$PATH:$SPARK_HOME/bin

# removes the Spark path from the PATH and unsets the system variable
PATH=$(echo $PATH| sed -e 's!'$SPARK_HOME'!!' -e 's/::/:/')
unset SPARK_HOME
```
## Spark Python
```bash
pyspark
exit()
```

## Datasets
[MovieLens datasets](https://grouplens.org/datasets/movielens/):
* [ml-100k.zip](http://files.grouplens.org/datasets/movielens/ml-100k.zip)
  * `u.data`: movie ratings
  * `u.item`: movie details
* [ml-100k.zip](http://files.grouplens.org/datasets/movielens/ml-1m.zip)
