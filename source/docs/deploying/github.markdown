---
layout: page
title: "Deploying with GitHub"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/github/
---
[Deploy Using GitHub User Pages](#github-user-pages)  
[Deploy Using Github Project Pages](#github-project-pages)  
[Custom Domains](#custom-domains)  

## Using GitHub User/Organization pages {#github-user-pages}

Use this if you want to host a site from `http://username.github.io` (though you can also use custom domains).

Create a new GitHub repository and name the repository with the format `username.github.io`, where `username` is your GitHub user name or organization name.

GitHub Pages for users and organizations uses the master branch like the public directory on a web server, serving up the files at your Pages URL `http://username.github.io`. As a result, you'll want to work on the source for your site in the source branch and commit the *generated content* to the master branch. Showcase has a configuration task that helps you set all this up.

~~~bash
$ rake setup_github_pages
~~~

The rake task will prompt you for a URL of the GitHub repo. Copy the SSH or HTTPS URL from your newly created repository (e.g. `git@github.com:username/username.github.io.git`) and paste as the response.

This will:

- Ask for and store your GitHub Pages repository URL.
- Rename the remote pointing to femmestem/showcase from 'origin' to 'Showcase'
- Add your GitHub Pages repository as the default origin remote.
- Switch the active branch from `master` to `source`.
- Configure your site's URL according to your repository.
- Setup a master branch in the `_deploy` directory for deployment.

Then, run

~~~bash
$ rake generate
$ rake deploy
~~~

This will generate your site, copy the generated files into the `_deploy/` directory, add them to git, and commit and push them up to the master branch. In a few seconds you should get an email from GitHub telling you that your commit has been received and will be published on your site.

**Don't forget** to commit the source for your site!

~~~bash
$ git add .
$ git commit -m 'your message'
$ git push origin source
~~~

**Note:** With new repositories, GitHub sets the default branch based on the branch you push first, and it looks there for the generated site content. If you're having trouble getting GitHub to publish your site, go to the admin panel for your repository and make sure that the master branch is the default branch.

## Using GitHub Project pages (gh-pages) {#github-project-pages}

GitHub's Project Pages service allows you to host a site for your existing open source project. GitHub will look for a `gh-pages` branch in your project's repository and make the contents available at URL `http://username.github.io/project`.

Here's how to can set up your Showcase site to publish to your projects gh-pages repository:

`$ rake setup_github_pages`

This will:

- Ask you for the repository URL for your project.
- Rename the remote pointing to femmestem/showcase from 'origin' to 'Showcase'
- Configure your site for deploying to a subdirectory.
- Set up a `gh-pages` branch for your project in the `_deploy/` directory, ready for deployment.

Then, run

~~~bash
$ rake generate
$ rake deploy
~~~

This will generate your site, copy the generated files into the `_deploy/` directory, add them to git, and commit and push them up to the master branch. In a few seconds you should get an email from GitHub telling you that your commit has been received and will be published on your site.

Now you have a place to commit the generated content for your site, but you should also set up repository to store the source for your site. After you set up a repository for your site source, add it as the origin remote.

~~~bash
$ git remote add origin {% raw %}<your repo url>{% endraw %} # set your new origin as the default branch
$ git config branch.master.remote origin
~~~

Now simply push your changes to update your site.

## Custom Domains

First you'll need to create a file named `CNAME` in your site's source:

~~~bash
$ echo 'your-domain.com' >> source/CNAME
~~~

OR

~~~bash
$ echo 'www.your-domain.com' >> source/CNAME
~~~

Next, you’ll need to visit your domain registrar or DNS host and add a record for your domain name.

For a sub-domain like www.example.com you would simply create a CNAME record pointing at `cat-mandu.github.io`.
If you are using a top-level domain like `example.com`, you must use an A record pointing to `192.30.252.153` or `192.30.252.154`.

**Do not use a CNAME record with a top-level domain!** It can have adverse side effects on other services, like email. Many DNS services will let you set a CNAME on a TLD, even though you shouldn’t.

Also, remember that it may take up to a full day for DNS changes to propagate, so be patient.

*Source:* [GitHub's Pages guide](https://help.github.com/categories/github-pages-basics/)

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)

## Next Steps
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/) 
