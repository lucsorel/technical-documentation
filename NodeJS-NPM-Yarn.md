# NodeJS and NPM installation

* when upgrading from an older version, uninstall ``nodejs`` and ``npm`` beforehand:
```bash
sudo apt-get purge nodejs npm
```

* install from PPA
In Debian distributions, NodeJS and NPM can be installed and updated from the [NodeJS dedicated APT repository](http://doc.ubuntu-fr.org/nodejs):

```bash
sudo apt-get install curl
# for 6.x LTS versions
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
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
outdated: lists the dependencies which are out-of-date
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

# Yarn
From [official installation page](https://yarnpkg.com/lang/en/docs/install/):

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn
```

See the [commands documentation](https://yarnpkg.com/en/docs/usage).

sudo apt-get update sometimes fails because of the GPG key which needs to be updated once in a while. Updating it with the following command solves the issue ([source](curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -)):

```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
```
