---
layout: page
title: "Setup"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/setup/
---

[Next: Configuration &raquo;](/docs/configuring)

## Requirements  
1. [Git](http://git-scm.com/)
2. Ruby 1.9.3 or greater using either [RVM](/docs/setup/rvm) or [rbenv](/docs/setup/rbenv)
3. [ExecJS](https://github.com/sstephenson/execjs){:target="_blank"} supported JavaScript runtime

To check your ruby version, run `$ ruby --version`.  
If your version is at least Ruby 1.9.3, then you're good to go. Otherwise, install or update your ruby version with [RVM](/docs/setup/rvm) or [rbenv](/docs/setup/rbenv).

## Set Up Showcase  

[Download](https://github.com/femmestem/Showcase/archive/master.zip) or clone from Github  

~~~ bash
$ git clone https://github.com/femmestem/Showcase.git showcase
$ cd showcase
~~~

Install dependencies  
**Note:** You will need to do this every time you update your version of Ruby.

~~~ bash
$ gem install bundler
$ rbenv rehash # rehash rbenv to run bundle command, skip if using RVM
$ bundle install
~~~

Install the default Showcase theme

~~~ bash
$ rake install
~~~

To verify the install was successful and preview your new site  

~~~ bash
$ rake preview
~~~

Open `localhost:4000` in an internet browser. You should see something like this:

![Showcase Landing Page](/images/docs/showcase_index.png)

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)

## Next Steps
[Configuring](/docs/configuring)  
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/)    
[Deploying](/docs/deploying)   
{% comment %}
[Themes & Customization](/docs/customizing)  
[3rd Party Plugins](/docs/plugins)  
{% endcomment %}


