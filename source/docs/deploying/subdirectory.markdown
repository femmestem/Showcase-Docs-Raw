---
layout: page
title: "Subdirectory"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/subdirectory/
---

Showcase can be deployed as a standalone site or deployed to a subdirectory of another site. If you're deploying to a subdirectory on your site, or if you're using Github's project pages, make sure you set up your URLs correctly in your configs. You can do this *almost* automatically:

`$ rake set_root_dir[your/path]`
 
(To reset Showcase as your main site: `$ rake set_root_dir[/]`)

Then, update your `_config.yml`:

{% coderay lang:yaml _config.yml %}
url: http://www.your-site.com/your/path
{% endcoderay %}
 
If deploying with rsync, update your `Rakefile`:
{% coderay Rakefile lang:ruby %}
document_root = "~/your-site.com/your/path"
{% endcoderay %}

## Manual Configuration

To manually configure deployment to a subdirectory, change `_config.yml`, `config.rb`, and `Rakefile`. 

### Example

Let's say Cat Mandu has a professional reputation in different industries, as a software developer and a commercial photographer. She wants to deploy Showcase as a subdirectory with portfolio and blog dedicated to her software development career. 

Existing site: `http://www.cat-mandu.com`
Subdirectory where Showcase will be deployed: `http://www.cat-mandu.com/software-developer`

**For Setting Up Relative Paths and URLs**
{% coderay lang:yaml _config.yml %}
# ----------------------- #
#      Main Configs       #
# ----------------------- #
url: http://www.cat-mandu.com/software-developer
root: /software-developer
destination: public/software-developer

# ------------------- #
#    Blog Configs     #
# ------------------- #
subscribe_rss: /software-developer/blog/atom.xml
{% endcoderay %}
 
**For Compass and Sass**
{% coderay lang:ruby _config.rb %}
http_path        = "/software-developer"
http_images_path = "/software-developer/images"
http_fonts_path  = "/software-developer/fonts"
css_dir          = "public/software-developer/stylesheets"
{% endcoderay %}
 
**For Generating Public-Facing Pages**
{% coderay Rakefile lang:ruby %}
public_dir       = "public/software-developer"

# If deploying with rsync, update your Rakefile path
document_root    = "~/cat-mandu.com/software-developer"
{% endcoderay %}

<br><br>
Credit: [Christine Feaster](https://github.com/femmestem/), [Brandon Mathis](https://github.com/imathis/)
