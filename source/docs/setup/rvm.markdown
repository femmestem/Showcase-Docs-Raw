---
layout: page
title: "Installing Ruby with RVM"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/setup/rvm/
---
RVM (Ruby Version Manager) handles the installation and management of multiple Ruby environments. Ruby 1.9.3 or above is required for Showcase, and RVM makes installation easy.

## Install RVM

Run the following command from your terminal.

`$ curl -L https://get.rvm.io | bash -s stable --ruby`

Be sure to follow any subsequent instructions as guided by the installation process.

## Install Ruby

Next install Ruby (at least 1.9.3) and you'll be all set.

~~~bash
$ rvm install ruby
$ rvm use 1.9.3
$ rvm rubygems latest
~~~

Run `ruby --version` to be sure you're using at least Ruby 1.9.3. If you're having trouble, seek help [here](https://rvm.io/support).

<br><br>
Credit: [Brandon Mathis](https://github.com/imathis/)

[&laquo; Return to Setup](/docs/setup/)
