---
layout: single
title: "Django Environment Setup"
categories: note
tags: [django]
author_profile: false
search: true
use_math: true
---

### Mac

Install [VSCode](https://code.visualstudio.com)

Install [Homebrew](https://brew.sh)

Install pyenv, pyenv-virtualenv

```zsh
brew install pyenv
```

setup pyenv

for bash

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init --path)"' >> ~/.profile
echo 'if [ -n "$PS1" -a -n "$BASH_VERSION" ]; then source ~/.bashrc; fi' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

```

for zsh

```zsh
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

```

### Windows

Install [VSCode](https://code.visualstudio.com)

Install WSL:

search 'windows 기능' - windows 기능 켜기/끄기 - check 'Linux용 windows 하위 시스템 항목' - restart - search 'store' - microsoft store - search 'ubuntu' - install ubuntu

```zsh
sudo apt-get update
```

```zsh
sudo apt-get install -y make build-essential \
libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev \
wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev git python-pip sqlite3
```

Install WSL - Remote in VSCode

```zsh
curl https://pyenv.run | bash
```

Install pyenv, pyenv-virtualenv

for bash

```bash
sed -Ei -e '/^([^#]|$)/ {a \
export PYENV_ROOT="$HOME/.pyenv"
a \
export PATH="$PYENV_ROOT/bin:$PATH"
a \
' -e ':a' -e '$!{n;ba};}' ~/.profile
```

```bash
echo 'eval "$(pyenv init --path)"' >>~/.profile

echo 'eval "$(pyenv init -)"' >> ~/.bashrc

echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

```

for zsh

```zsh
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zprofile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init --path)"' >> ~/.profile

echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

```

### After

Install [Python](https://www.python.org)

```zsh
pyenv install --list
```

and choose a version

```zsh
pyenv virtualenv [version] [name]
```

Install django

```zsh
pip3 install django==[version]
```

#### set virtual environmnet

Move to directory that you want to work and

```zsh
pyenv local [name]
```

#### Creating project

```zsh
django-admin startproject [project-name]
```

##### Run Server

move to 'project-name'

```zsh
manage.py runserver
```
