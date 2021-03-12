# Environment Setup Instructions for Linux

This guide will walk you through how to set up your machine for local software development. These instructions are
designed to be executed in order, and assume you have a fresh installation of Ubuntu.

This guide is written for:
    - Linux 5.4.0
    - Ubuntu 20.04.1

This guide will translate well for researchers using Mac OS systems. There are no plans to extend this guide for windows
operating systems.

---

## Shortcuts

- [Environment Setup Instructions for Linux](#environment-setup-instructions-for-linux)
  - [Shortcuts](#shortcuts)
  - [Homebrew](#homebrew)
  - [SSH Key](#ssh-key)
  - [Github](#github)
  - [Clone Repositories](#clone-repositories)
  - [Python](#python)
  - [Python Virtual Environment](#python-virtual-environment)
  - [Dev Environment Aliases](#dev-environment-aliases)
  - [Optional Quality of Life Tips](#optional-quality-of-life-tips)

---

## Homebrew

Install Homebrew. It can be installed in your home directory, in which case it does not use sudo. Homebrew does not
use any libraries provided by your host system, except glibc and gcc if they are new enough. Homebrew can install its
own current versions of glibc and gcc for older distributions of Linux. Run following to the terminal.

    ```shell
      sudo apt install curl
      sudo apt-get install git
      /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
      sudo apt-get install build-essential
      sudo apt-get update; sudo apt-get install --no-install-recommends make build-essential libssl-dev zlib1g-dev
      libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev
      libxmlsec1-dev libffi-dev liblzma-dev
      echo 'eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)' >> /home/{user_name}/.profile
      eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
      brew update
      brew upgrade
      brew install gcc
      brew doctor
    ```

## SSH Key

Generate your public/private id_rsa key. Skip the file location prompt by pressing enter and make a secure passphrase
when prompted

    ```shell
      ssh-keygen -t rsa -C {youremail@email.com}
    ```

update your ~/.ssh/config file to automatically load keys into the ssh-agent

    ```text
      Host *
        AddKeystoAgent yes
        IdentityFile ~/.ssh/id_rsa
    ```

Add your SSH private key to the ssh-agent and store your passphrase on your Keychain by typing the following in the
terminal

    ```shell
      ssh-add -K ~/.ssh/id_rsa
    ```

## Github

Ensure that you have received an invitation to the company github account.
Add your public key to your Github account so you can remotely interact with the companies Github repository.

For each repo, in github naviagte to "Personal Settings", select "SSH and GPG Keys", click "add new SSH key", and add
a title of your choice (ex: id_rsa). Run the following in your terminal to copy your key and paste in the "Key" section
on github.

Copy the SSH key to your clipboard.

    ```shell
      cat ~/.ssh/id_rsa.pub
    ```

Set up your author info in git

    ```shell
      git config --global user.name "Your Name"
      git config --global user.email "you@example.com"
    ```

Verify your global git configuration

    ```shell
      git config --global -l
    ```

## Clone Repositories

Clone Github repositories to your local development environment. Make a "code" directory within your home directory,
and clone all repositories from within the code directory:

    ```shell
      mkdir code
      cd ~/code

      git clone git@github.com:explore-meps/meps_dev.git
      git clone git@github.com:explore-meps/meps_analytics.git
      git clone git@github.com:explore-meps/meps_wiki.git
    ```

## Python

We use [pyenv](https://github.com/pyenv/pyenv) for Python version managment. pyenv allows us to install and switch
between specific python versions.

Clone pyenv into \$HOME/.pyenv through the terminal with:

    ```shell
      git clone https://github.com/pyenv/pyenv.git ~/.pyenv
    ```

Add the following line to you .bashrc

    ```text
      # pyenv setup
      export PYENV_ROOT="$HOME/.pyenv"
      export PATH="$PYENV_ROOT/bin:$PATH"
      eval "$(pyenv init -)"
    ```

Then restart the shell

Install Python 3.8.5 and set the global default version

    ```shell
      pyenv install 3.8.5
      pyenv global 3.8.5
    ```

## Python Virtual Environment

Python's package manager "pip" is installed for you when you install Python 2.7.12+ via pyenv. Run the following to
choose the version of Python you want to use in your virtual environment (3.8.5+ recommended):

    ```shell
      pyenv global 3.8.5
      pip install --upgrade pip
      pip install --upgrade setuptools
      pip install virtualenv
      pip install virtualenvwrapper
    ```

In the event you want to create multiple virtual environments that use different versions of Python, you will need to
repeat the above steps for each Python version, making sure that you are not in a virtual environment when you run the
steps.

Next add the following lines to you .bashrc **after** the `eval "$(pyenv init -)"` command to enable the virtual
environment wrapper for the globally installed python version, then restart your terminal:

    ```text
      export WORKON_HOME=$HOME/.virtualenvs
      export PROJECT_HOME=$HOME/meps
      source $(pyenv prefix)/bin/virtualenvwrapper.sh
    ```

To create new virtual environments, run the following in your terminal

    ```shell
      pyenv global 3.8.5 # choose the version of python for the virtual environment

      # analytics
      mkvirtualenv meps_analytics
      cd ~/meps/meps_analytics
      pip install -r requirements.txt

      # development
      mkvirtualenv meps_dev
      cd ~/meps/meps_dev
      pip install -r requirements.txt
    ```

## Dev Environment Aliases

Add the following dev environment aliases to the bottom your .bashrc file to allow quick access to differnt virtual environments

    ```shell
      # dev environment aliases
      alias meps_dev='cd ~/meps/meps_dev; workon meps_dev'
      alias meps_an='cd ~/meps/meps_analytics; workon meps_analytics'
      alias meps_wiki='cd ~/meps/meps_wiki; workon meps_wiki'
      alias code='code -n .'
      alias jn='jupyter notebook'
    ```

## Optional Quality of Life Tips

Press the up and down arrows while in shell to autocomplete commands based on user history. Enforce by running the
following script outside of a virtual environment:

    ```shell
    cat >> ~/.inputrc <<'EOF'
    "\e[A": history-search-backward
    "\e[B": history-search-forward
    EOF
    ```
