---
layout: page
title: "Deploying with Heroku"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/heroku/
---
## Requirements 
1. [Heroku account](https://signup.heroku.com/identity) (it's free!)

## Step 1
First, install the Heroku gem

~~~bash
$ gem install heroku
~~~

## Step 2
Create a Heroku app for deployment. If this is your first time using Heroku, this command will ask for your account credentials and automatically upload your public SSH key. If you don't already have a public key, follow this [GitHub guide](https://help.github.com/articles/generating-ssh-keys/) to create one.

~~~bash
$ heroku create
~~~

This will create a new Heroku app for you to deploy to, and it will add a git remote named 'heroku'.

## Step 3
Set `heroku` as the default remote for push/fetch

~~~bash
$ git config branch.master.remote heroku
~~~

Edit the `.gitignore` in the root of your repository by removing `public` and `Gemfile.lock`. This will let you add *generated content* to deploy to Heroku.

~~~bash
$ rake generate
$ git add .
$ git commit -m 'site update'
$ git push heroku master
~~~

That's it, you just deployed to Heroku. If you want to set up a custom domain, check out the [Heroku docs](https://devcenter.heroku.com/articles/custom-domains).

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)

## Next Steps
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/) 
