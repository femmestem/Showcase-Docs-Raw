---
layout: page
title: "Deploying with Rsync"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/rsync/
---
## Deploying with Rsync via SSH

Add your server configurations to the `Rakefile` under Rsync deploy config. To deploy with Rsync, be sure your public key is listed in your server's `~/.ssh/authorized_keys` file.

~~~ruby
ssh_user       = "user@domain.com"
document_root  = "~/yoursite.com/"
rsync_delete   = true
deploy_default = "rsync"
~~~

Now when you run the `generate` and `deploy` commands, your public directory will be synced to your server's document root.

~~~bash
$ rake generate   # If you haven't generated your site yet
$ rake deploy     # Syncs your site via SSH
~~~

## Note on Rsync Delete

If you choose to delete on sync, Rsync will create a 1:1 match. Files will be added, updated and deleted from your deploy directory to mirror your local copy.

If you do not choose to delete:

- You can store files beneath your site's `_deploy/` directory, which aren't found in your local version.
- Files you have removed from your local site must be removed manually from the server.

### Excluding Files from Sync

If you would like to keep your Showcase files synced but also want the convenience of keeping some files or directories on the server without having to mirror them locally, you can exclude them from Rsync.

When syncing, Rsync can exclude files or directories locally or on the server. Simply add an `rsync-exclude` file to the root directory of your site project like this:

{% coderay rsync-exclude lang:ruby %}
some-file.txt
some-directory/
*.mp4
{% endcoderay %}

Note: using excludes will prevent rsync from uploading local files, or if the delete option is specified, it will prevent rsync from deleting excluded items on the server.

## Version control

You'll want to keep your site source in a remote git repository. Set up a [GitHub repository](https://github.com/new) or host your own, then follow the steps below.

~~~bash
$ git remote rename origin showcase # Since you cloned Showcase, you'll need to change the origin remote
$ git remote add origin {% raw %}<your-repository-url>{% endraw %}
$ git config branch.master.remote origin # set your new origin as the default branch
~~~

### Host Your Own Remote Repository

If you want to set up a private git repository on your own server, here's how to do it. You'll need SSH access to follow along.

~~~bash
$ ssh user@host.com
$ mkdir -p git/showcase.git
$ cd git/showcase.git
$ git init --bare
$ pwd  # print the working directory, you'll need it for next step
$ logout
~~~

The URL for your remote repository is `ssh://user@host.com/{% raw %}<output of pwd above>{% endraw %}`

## Deploying to a Subdirectory

To host a Showcase site as a subdirectory of another site, e.g. `http://yoursite.com/your-showcase-site/`, you would need to configure Showcase for [deploying to a subdirectory](/docs/deploying/subdirectory).

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)

## Next Steps
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/) 
