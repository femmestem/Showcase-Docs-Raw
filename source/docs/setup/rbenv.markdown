---
layout: page
title: "Installing Ruby with Rbenv"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/setup/rbenv/
---

Rbenv handles the installation and management of multiple Ruby environments. Ruby 1.9.3 or above is required for Showcase, and Rbenv makes installation easy.

## Standard Rbenv Installation

The standard method for installing rbenv uses Git. From your terminal, run the following commands:

~~~bash
$ cd
$ git clone git://github.com/sstephenson/rbenv.git .rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
$ git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
$ source ~/.bash_profile
~~~

**Zsh users:** In the instructions above substitute `~/.bash_profile` with `~/.zshenv`.

**Note:** You may need to add `source ~/.bash_profile` to `~/.profile` depending upon your bash configuration.

## Alternate Installation Using Homebrew

If you use Homebrew on Mac OS X you may prefer to install rbenv like this:

~~~bash
$ brew update
$ brew install rbenv
$ brew install ruby-build
~~~

## Install Ruby

Next install Ruby (at least 1.9.3) and you'll be all set.

~~~bash
$ rbenv install 1.9.3-p0
$ rbenv local 1.9.3-p0
$ rbenv rehash
~~~

**Note:** `rbenv local 1.9.3-p0` ensures that your Showcase installation is using Ruby 1.9.3-p0 without modifying your environment in any other directory. If you want to use 1.9.3-p0 everywhere, run `$ rbenv global 1.9.3-p0` instead.

Run `ruby --version` to be sure you're using at least Ruby 1.9.3. If you're having trouble, seek help [here](https://github.com/sstephenson/rbenv/issues).

<br><br>
Credit: [Brandon Mathis](https://github.com/imathis/)

[&laquo; Return to Setup](/docs/setup/)
