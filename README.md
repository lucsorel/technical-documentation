# Technical documentation
My online technical documentation. May it be useful for anyone too :)

## Free disk space
From this [cleanup unused Linux kernels in Ubuntu](http://markmcb.com/2013/02/04/cleanup-unused-linux-kernels-in-ubuntu/) article. Run this if you've rebooted after installing a new kernel:
```bash
dpkg -l 'linux-*' | sed '/^ii/!d;/'"$(uname -r | sed "s/\(.*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^ ]*\).*/\1/;/[0-9]/!d' | xargs sudo apt-get -y purge
```

## SFR wifi connection
* (de)activate wifi [SHA-1](http://www.freeformatter.com/message-digest.html)
* [HTG Explains: The Difference Between WEP, WPA, and WPA2 Wireless Encryption (and Why It Matters)](http://www.howtogeek.com/167783/htg-explains-the-difference-between-wep-wpa-and-wpa2-wireless-encryption-and-why-it-matters/)
* [Comment gérer votre connexion WiFi avec l'interface web http://192.168.1.1 ?](http://assistance.sfr.fr/runtime/internet-et-box/box-nb6/gerer-wifi-interface-web-192.html)
