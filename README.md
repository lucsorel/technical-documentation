# Technical documentation
My online technical documentation. May it be useful for anyone too :)

## Free disk space
From this [cleanup unused Linux kernels in Ubuntu](http://markmcb.com/2013/02/04/cleanup-unused-linux-kernels-in-ubuntu/) article. Run this if you've rebooted after installing a new kernel:
```bash
dpkg -l 'linux-*' | sed '/^ii/!d;/'"$(uname -r | sed "s/\(.*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^ ]*\).*/\1/;/[0-9]/!d' | xargs sudo apt-get -y purge
```
