---
layout: page
title: "Configuring Showcase"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/configuring/
---

[&laquo; Previous: Setup](/docs/setup)

Showcase is nearly ready to be deployed out of the box. To keep things simple, the configurations for site content and third-party plugins are contained in a single file: `_config.yml`. Here's a list of files for configuring Showcase:

~~~ bash
_config.yml         # Main config (Jekyll and third-party plugins)
Rakefile            # Deployment config
config.rb           # Compass config
config.ru           # Rack config
~~~

Configurations in the `Rakefile` are mostly related to deployment and you probably won't have to touch them unless you're using rsync.

## Main Configuration

{% coderay lang:yaml _config.yml %}
# ----------------------- #
#      Main Configs       #
# ----------------------- #

url:                # For rewriting urls for RSS, etc.
title:              # Used in the header and title tags
subtitle:           # A short description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
description:        # Default meta description for your site that
                    # appears with your site link in search engine results
date_format:        # Format dates using Ruby's date strftime syntax
{% endcoderay %}

**Note:** If your site will have a multi-author blog, you may want to set `author:` to the name of your company or project, and add author metadata to the [YAML front matter](/docs/blogging#anatomy-of-posts){:target="_new"} configurations inside posts and pages to give proper attribution for those works.

## Jekyll Configuration

{% coderay lang:yaml _config.yml line_number_start:19 %}
# --------------------- #
#    Jekyll Configs     #
# --------------------- #

root:               # Mapping for relative urls (default: /)
source:             # Directory for site source files
destination:        # Directory for generated site files
plugins:            # Directory for Jekyll plugins
code_dir:           # Directory for code snippets (for include_code plugin)
{% endcoderay %}

If you want to publish your site to a subdirectory, (see [Deploying Showcase to a Subdirectory]()).


## Portfolio Configuration
Portfolio functionality is built on [Jekyll's Collections](http://jekyllrb.com/docs/collections/) feature. Portfolio configurations are updated for you automatically with the `new_portfolio` rake task. This section is just FYI to troubleshoot a portfolio page is not being published properly.

{% coderay lang:yaml _config.yml line_number_start:38 %}
# ------------------------------- #
#    Portfolios & Collections     #
# ------------------------------- #

collections:
  portfolio-name:  # Registers documents in _portfolio-name directory as a collection
    output:        # Create public-facing web page for documents in portfolio directory 
    permalink:     # Permalink structure for portfolio and project pages 
{% endcoderay %}

## Blog Configuration

{% coderay lang:yaml _config.yml line_number_start:62 %}
# ------------------- #
#    Blog Configs     #
# ------------------- #

subscribe_rss:      # URL for your site's feed, defauts to /blog/atom.xml
subscribe_email:    # URL to subscribe by email (service required)
email:              # Optional email address for the RSS feed
category_feeds:     # Enable per category RSS feeds (defaults to false)

permalink:         # Permalink structure for blog posts
paginate:          # Posts per page on the blog index
paginate_path:     # Directory base for pagination URLs eg. /blog/page/2/
recent_posts:      # Number of recent blog posts to appear in the sidebar
category_dir:      # Directory for generated blog category pages
{% endcoderay %}

## Sidebar Modules

{% coderay lang:yaml _config.yml line_number_start:81 %}
# ---------------------- #
#    Sidebar Modules     #
# ---------------------- #

default_asides:    # Configure what shows up in the sidebar and in what order
blog_index_asides: # Optional sidebar config for blog index page
post_asides:       # Optional sidebar config for post layout
page_asides:       # Optional sidebar config for page layout
{% endcoderay %}

## Plugin Settings

These third party integrations are already set up for you. Simply fill in the configurations and they'll be added to your site.

{% coderay lang:ruby _config.yml line_number_start:95 %}
# ----------------------- #
#   3rd Party Settings    #
# ----------------------- #

Github             # List your github repositories in the sidebar
Twitter            # Add a button for sharing posts and pages on Twitter
Google Plus One    # Setup sharing for posts and pages on Google's Plus One network.
Pinboard           # Share your recent Pinboard bookmarks in the sidebar.
Delicious          # Share your recent Delicious bookmarks in the sidebar.
Disqus Comments    # Add your Disqus short name to enable Disqus comments on your site.
Google Analytics   # Add your tracking ID to enable Google Analytics tracking for your site.
Facebook           # Add a Facebook 'Like' button
{% endcoderay %}

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)

## Next Steps
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/)  
[Deploying](/docs/deploying/)  
{% comment %} 
[Themes & Customization](/docs/customizing/)  
[3rd Party Plugins](/docs/plugins/)
{% endcomment %}
