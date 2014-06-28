# tilde

$HOME is where the heart is. Manage it with class.

## Purpose

The purpose of `tilde` is to define an easily adoptable directory structure for dotfiles projects. The reason for having a common directory structure across projects is to make merging other people’s dotfiles into your own a breeze. In addition to managing and setting up your dotfiles, `tilde` provides package management and allows you to extend the install by way of a easy to follow YAML file.

## Installation

To install `tilde`, run this from the command-line:

	TODO

## Directory Structure and Files

To leverage `tilde`’s symlinking capabilities you will need to conform to the following directory structure. The directories and files list here are optional, so only include what you want. Also be aware that you can include any additional directories and/or files that you’d like. They will simply be ignored unless you have specified commands in your `tilde.yml`.

	.
	├── bash/
	│   ├── bash_profile
	│   └── bashrc
	├── bin/
	│   └── ...
	├── git/
	│   ├── hooks/
	│   │   └── ...
	│   ├── scripts/
	│   │   └── ...
	│   └── gitconfig
	├── hg/
	│   └── hgrc
	├── launchd/
	│   └── ...
	├── mutt/
	│   └── muttrc
	├── vim/
	│   └── vimrc
	├── zsh/
	│   ├── themes/
	│   │   └── ...
	│   └── zshrc
	└── tilde.yml

## Configuration

If you are using the package management functionality and/or specifying additional commands you will need to include `tilde.yml` in the root of your project.

	packages:
	  brew:
	    - Homebrew/homebrew-php
	    - mysql
	      - launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
	      - launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
	    - wget
	  gem:
	    - sass
	  npm:
	    - less@1.3

Packages are listed in the `packages:` section of the file, grouped by package manager. `tilde` supports `apt` (`apt-get` or `aptitude`), `brew`, `gem` and `npm`, feel free to fork and add in your preferred package manager if it’s not there. After each package, you can list out any commands that need to be run after the package is installed. The packages themselves are installed in the order that they are listed in the file, be mindful of this to avoid any dependency problems. Please note that `brew` accepts both taps and packages and that `npm` packages are installed with the `-g` flag to install them globally.

## Usage

### Installing dotfiles

	tilde install username/repository

Clones the specified GitHub repository to `~/.tilde/username/respository`, symlinks the files and directories, installs packages and runs any additional commands specified in the `tilde.yml` file.

### Updating / reinstalling currently installed dotfiles

	tilde update

Pulls down changes from the remote GitHub repository, re-symlinks files and directories, installs all packages and runs all additional commands specified in the `tilde.yml` file (new and existing).

### Merging from another repository

	tilde merge username/repository

Attempts to merge the entire repository into your currently installed dotfiles. If there are existing files, you will be prompted to merge them manually. Upon completion your installed dotfiles will be commited and pushed back to your remote GitHub repository.

	tilde merge username/repository/path/to/file/or/directory

Attempts to merge the specified file or directory into your currently installed dotfiles. If there are existing files, you will be prompted to merge them manually. Upon completion, your installed dotfiles will be commited and pushed back to your remote GitHub repository.

### Save changes to your installed dotfiles

	tilde save

If there are any manual changes to your dotfiles, they will be commited and pushed to your remote GitHub repository.
