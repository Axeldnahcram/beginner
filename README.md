# Acuity macOS Dev Setup

This document describes how Acuity devs and datascientists set up their developer environments on a new MacBook or iMac for Acuity. We will set up [Python](http://www.python.org/). 

The document assumes you are new to Mac, but can also be useful if you are reinstalling a system and need some reminder. The steps below were tested on **macOS High Sierra** (10.13), but should work for more recent versions as well.

**Contributing**: If you find any mistakes in the steps described below, or if any of the commands are outdated, do let me know! For any other suggestions, please understand if I don't include everything. This guide was originally written for some friends getting started with programming on a Mac, and as a personal reference for myself. I'm trying to keep it simple!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Security](#security)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Git](#git)
- [Visual Studio Code](#visual-studio-code)
- [Vim](#vim)
- [Python](#python)
- [Pack office](#pack-office)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > About This Mac** then **Software Update...**.

## System preferences

If this is a new computer, there are a couple of tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock
- Hot corners > Set up a way to easely put your mac to sleep

## Security

I recommend checking that basic security settings are enabled. You will be happy to have done so if ever your Mac is lost or stolen.

In **Apple Icon > System Preferences**:

- Users & Groups: If you haven't already set a password for your user during the initial set up, you should do so now
- Security & Privacy > General: Require password immediately after sleep or screen saver begins (you can keep a grace period of a couple minutes if you prefer, but I like to know that my computer locks as soon as I close it)
- Security & Privacy > FileVault: Make sure FileVault disk encryption is enabled
- iCloud: If you haven't already done so during set up, enable Find My Mac

## iTerm2

### Install

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm2 > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Under the section **General** set **Working Directory** to be **Reuse previous session's directory**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in macOS preference panes). Close the window and open a new one to see the size change.

### Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place.
If you are confortable with bash you can keep it. But I prefer to use [Oh My ZSH](https://ohmyz.sh/)

All you need is to open your terminal and execute this 
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). 
The most popular one for macOS is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Developer Tools** for **Xcode**. These include compilers that will allow you to build things from source. You can install them directly from the terminal with:

```
xcode-select --install
```

Once that is done, we can install Homebrew by copy-pasting the installation command from the [Homebrew homepage](http://brew.sh/) inside the terminal:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Follow the steps on the screen. You will be prompted for your user password so Homebrew can set up the appropriate permissions.

Once installation is complete, you can run the following command to make sure everything works:

```
brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```
brew install <formula>
```

To see if any of your packages need to be updated:

```
brew outdated
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to rollback. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```
brew cleanup
```

To see what you have installed (with their version numbers):

```
brew list --versions
```

### Homebrew Services

A nice extension to Homebrew is [Homebrew Services](https://github.com/Homebrew/homebrew-services). It will automatically launch things like databases when your computer starts, so you don't have to do it manually every time.

Homebrew Services will automatically install itself the first time you run it, so there is nothing special to do.

After installing a service (for example a database), it should automatically add itself to Homebrew Services. If not, you can add it manually with:

```
brew services <formula>
```

Start a service with:

```
brew services start <formula>
```

At anytime you can view which services are running with:

```
brew services list
```

## Git

macOS comes with a pre-installed version of [Git](http://git-scm.com/), but we'll install our own through Homebrew to allow easy upgrades and not interfere with the system version. To do so, simply run:

```
brew install git
```

When done, to test that it installed fine you can run:

```
which git
```

The output should be `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

```
cd ~
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig
```

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

If you want more information with git make sure to follow our git tutorial.

## Pycharm

If you already have your own IDE and you are comfortable with it keep it. Otherwise, you might want to download
[Pycharm](jetbrains.com/fr-fr/pycharm/download/#section=mac)

After downloading it, you can add a few shortcuts to make it more useful. First, 

- Pycharm > Preferences > Keymap > Main menu > Code > Comment: change it so that commenting is easy
- Pycharm > Preferences > Keymap > Main menu > Code > Reformat: it automatically Pep8 your code, no matter how dirty it is

## Vim

Although Pycharm will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. Also, it is good to know that typing `:x` when in Normal mode will save and exit. After that, it's just remembering a few important keys.

Vim's default settings aren't great, and you could spend a lot of time tweaking your configuration (the `.vimrc` file). But if you only use Vim occasionally, you'll be happy to know that [Tim Pope](https://github.com/tpope) has put together some sensible defaults to quickly get started.

Using Vim's built-in package support, install these settings by running:

```
mkdir -p ~/.vim/pack/tpope/start
cd ~/.vim/pack/tpope/start
git clone https://tpope.io/vim/sensible.git
```

With that, Vim will look a lot better next time you open it!

## Python

macOS, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version using [pyenv](https://github.com/yyuu/pyenv). This will also allow us to manage multiple versions of Python (ex: 2.7 and 3) should we need to.

Install `pyenv` via Homebrew by running:

```
brew install pyenv
```

When finished, you should see instructions to add something to your profile. Open your `.zshrc` in the home directory (you can use `code ~/.zshrc`), and add the following line:

```bash
if command -v pyenv 1>/dev/null 2>&1; then eval "$(pyenv init -)"; fi
```

Save the file and reload it with:

```
source ~/.bash_profile
```

Before installing a new Python version, the [pyenv wiki](https://github.com/pyenv/pyenv/wiki) recommends having a few dependencies available:

```
brew install openssl readline sqlite3 xz zlib
```

We can now list all available Python versions by running:

```
pyenv install --list
```

Look for the latest 3.x version (or 2.7.x), and install it (replace the `.x.x` with actual numbers):

```
pyenv install 3.x.x
```

List the Python versions you have locally with:

```
pyenv versions
```

The star (`*`) should indicate we are still using the `system` version, which is the default. I recommend leaving it as the default as some [Node.js](https://nodejs.org/en/) packages will use it in their installation process.

You can switch your current terminal to another Python version with:

```
pyenv shell 3.x.x
```

You should now see that version when running:

```
python --version
```

In a project directory, you can use:

```
pyenv local 3.x.x
```

This will save that project's Python version to a `.python-version` file. Next time you enter the project's directory from a terminal, `pyenv` will automatically load that version for you.

For more information, see the [pyenv commands](https://github.com/yyuu/pyenv/blob/master/COMMANDS.md) documentation.

### pip

[pip](https://pip.pypa.io) was also installed by `pyenv`. It is the package manager for Python.

Here are a couple Pip commands to get you started. To install a Python package:

```
pip install <package>
```

To upgrade a package:

```
pip install --upgrade <package>
```

To see what's installed:

```
pip freeze
```

To uninstall a package:

```
pip uninstall <package>
```

### virtualenv

[virtualenv](https://virtualenv.pypa.io) is a tool that creates an isolated Python environment for each of your projects.

For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder, that will be managed by `virtualenv`. The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally.

Instead of installing and using `virtualenv` directly, we'll use the dedicated `pyenv` plugin [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv) which will make things a bit easier for us. Install it via Homebrew:

```
brew install pyenv-virtualenv
```

After installation, add the following line to your `.bash_profile`:

```bash
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

And reload it with:

```
source ~/.zshrc
```

Now, let's say you have a project called `myproject`. You can set up a virtualenv for that project and the Python version it uses (replace `3.x.x` with the version you want):

```
pyenv virtualenv 3.x.x myproject
```

See the list of virtualenvs you created with:

```
pyenv virtualenvs
```

To use your project's virtualenv, you need to **activate** it first (in every terminal where you are working on your project):

```
pyenv activate myproject
```

If you run `pyenv virtualenvs` again, you should see a star (`*`) next to the active virtualenv.

Now when you install something:

```
pip install <package>
```

It will get installed in that virtualenv's folder, and not conflict with other projects.

You can also set your project's `.python-version` to point to a virtualenv you created:

```
pyenv local myproject
```

Next time you enter that project's directory, `pyenv` will automatically load the virtualenv for you.

### Anaconda and Miniconda

The Anaconda/Miniconda distributions of Python come with many useful tools for scientific computing.

You can install them using `pyenv`, for example (replace `x.x.x` with an actual version number):

```
pyenv install miniconda3-x.x.x
```

After loading an Anaconda or Miniconda Python distribution into your shell, you can create [conda](https://docs.conda.io/) environments (which are similar to virtualenvs):

```
pyenv shell miniconda3-x.x.x
conda create --name  mycondaproject
conda activate mycondaproject
```

Install packages, for example the [Jupyter Notebook](https://jupyter.org/), using:

```
conda install jupyter
```

You should now be able to run the notebook:

```
jupyter notebook
```

Deactivate the environment, and return to the default Python version with:

```
conda deactivate
pyenv shell --unset
```

## Pack Office

Download every single office app. You should have received the link by mail.

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Chrome](https://www.google.com/chrome/): No comment
- [Knime](https://www.knime.com/download-installer/8/64bit): The old models are probably made on knime, you should not have to use it but just in case
- [Docker](https://www.docker.com/): Probably the best thing that ever existed, allows you to develop and create isolated environments **(free)**
- [Password](https://www.lastpass.com/): Securely store your login and passwords, and access them from all your devices. **(free)**
- [Postman](https://www.getpostman.com/): Easily make HTTP requests. Useful to test your REST APIs. **(Free for basic features)**
- [Versioning](https://www.sourcetreeapp.com/): I do everything through the `git` command-line tool, but I like to use Sourcetree just to review the diff of my changes. **(Free)**
