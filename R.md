# R installation tips
* installation of the base R package:
```bash
sudo apt-get install r-base
```

* required for the installation of the `XML` R library

```bash
# in a terminal:
sudo apt-get install libxml2-dev
# in the R console:
install.packages('XML')
```

* required for the installation of the `XLSX` R library, which requires the Java wrapper for R, in order to use Java libraries to handle xlsx files (from [Installing and loading xlsx package in R with Ubuntu](https://orajavasolutions.wordpress.com/2014/06/03/installing-and-loading-xlsx-package-in-r-with-ubuntu/))

```bash
# in a terminal:
sudo updatedb
locate libjvm.so # gives the path to the libjvm.so
sudo ln -s /real/path/to/libjvm.so /usr/lib
sudo apt-get install r-cran-rjava
# in the R console:
install.packages('xlsx')
```
