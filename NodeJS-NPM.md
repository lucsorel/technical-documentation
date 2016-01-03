# NodeJS and NPM installation
* install from PPA
In Debian distributions, NodeJS and NPM can be installed and updated from the [NodeJS dedicated APT repository](http://doc.ubuntu-fr.org/nodejs):

```bash
sudo apt-get install curl
# for 4.x LTS versions
curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -
# for 5.x latest versions
curl -sL https://deb.nodesource.com/setup_5.x | sudo bash -
sudo apt-get install nodejs
```

# NPM tips
## Abbreviate commands and flags
http://blog.izs.me/post/1675072029/10-cool-things-you-probably-didnt-realize-npm
* NPM commands
```
i: install
r, rm: uninstall
ln: link
ls: list
bn: bundle
up: update
c: config
```

* NPM flags
```
-S: save as dependency
-D: save as dev dependency

# command + flag
## will install only dependencies
npm install --production
## removes the dev dependencies (after a full installation + tests in a continuous integration environment)
npm prune --production
```

## Publishing Node.js packages
See https://semaphoreci.com/community/tutorials/npm-node-js-package-manager

Because every package is just a directory with package.json file and some other files, you can package your project, share it with the community and collaborate.

First you need to register yourself within NPM registry from the terminal and provide username, password and email address.
```
npm adduser
```

Now that you have an account you go to root of your to-be-published project and do:

```
npm publish
```

## NPM as a build tool
http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/
