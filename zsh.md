
# Install ZSH

```zsh
# installs packages
sudo apt-get install zsh git-core

# configures zsh
zsh
# -> 0: creates ~/.zshrc

# sets zsh by default
chsh
```

# Install oh-my-zsh

From [the official documentation](https://github.com/robbyrussell/oh-my-zsh#basic-installation)

```sh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
chsh -s `which zsh`
```

# Additional setup

* install he nvm plugin

```sh
nano ~/.zshrc

# add the nvm plugin
plugins=(
  git
  nvm
)
```
