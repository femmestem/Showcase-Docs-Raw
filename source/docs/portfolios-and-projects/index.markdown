---
layout: page
title: "Portfolios and Projects"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/portfolios-and-projects/
---
Showcase portfolio pages display an album cover style list of projects. When you create a new project page inside the portfolio folder, it will automatically be added to the portfolio index page.

Showcase includes rake tasks that set up this functionality for you by creating pages preloaded with metadata, and registering portfolios in the `_config.yml` and `source/_data/collections.yml` files.

**Note:** If you are using zsh in the command line, then add `alias rake=noglob rake` to your zsh config to prevent the `zsh: no matches found` error that occurs when running these rake tasks.

Some command line interpreters, e.g. zsh, have a special meaning for `[` and `]`. For rake tasks with options `$ rake task_name[option]`, you have to escape the brackets or temporarily switch to bash.

Go to:  
[Anatomy of Pages](#anatomy-of-pages)  
[Portfolios](#portfolios)  
[Projects](#projects)  
[Generate and Preview Site](#generate-and-preview-site)  


## Anatomy of Pages 
{% assign openTag = '{%' %}

Each page must include YAML front matter at the top (the content between two fences `---`) which tells Jekyll how to process pages. Attributes in the front matter can be accessed dynamically within the content area using Liquid templating language, e.g. `{% raw %}{% page.attributeName %}{% endraw %}`.

Below the front matter is the content area. Anything in the content area will appear on the page. By default, posts and pages are markdown files, which accept any combination of markdown syntax, plain text (interpreted as Markdown), HTML, and Liquid templating syntax.

To prevent a block of text from being parsed by the markdown preprocessor so that it appears as-is, enclose it between `{{ openTag }}{% raw %} raw %}{% endraw %}` and `{{ openTag }}{% raw %} endraw %}`{% endraw %} tags.

To keep comment text hidden from the rendered page, include it between `{% raw %}{% comment %}{% endraw %}` and `{% raw %}{% endcomment %}{% endraw %}` tags.

**Example**

See rendered page here: ["Anatomy of Pages" example](/docs/portfolios-and-projects/anatomy-of-pages/){:target="_new"}
{% coderay source/anatomy-of-pages/index.markdown %}
---
layout: page
title: "Anatomy of Pages"
comments: false
sharing: false
footer: false
---
{% raw %}
<h2> Anything Written Here Is Page Content </h2>
{% comment %}This text won't be rendered when you build the site.{% endcomment %}

<strong>This</strong> will render the same as **that**.

### You Can Render the Page's YAML Front Matter with Liquid

Page Title: {{ page.title }}    

### You Can Embed Code Snippets

{% codeblock %} 
def sayhello
    puts "Hello World!"
end
{% endcodeblock %}

...with syntax highlighting

{% codeblock lang:ruby %}
def sayhello
    puts "Hello World!"
end
{% endcodeblock %}

...and downloadable code snippets:

{% codeblock helloworld.rb http://mysite.com/helloworld.rb Download %}
    def sayhello
        puts "Hello World!"
    end
{% endcodeblock %}

{% endraw %}
{% endcoderay %}

## Portfolios   
A Showcase portfolio is a collection of project pages stored in `source/_portfolio-name/` and a portfolio index page. The index page generates a webpage at `http://www.site.com/portfolio-name/` that is populated with an album cover style list of projects. An album will only be created for projects listed for `projects:` in the [YAML front matter](#anatomy-of-pages) of the portfolio index page.

Album covers, icons, and links are configured in the **project's** YAML front matter ([see example](#project-example)).

Anything in the content section of the portfolio index page will appear before the list of projects.

**Note:** Showcase does not support a portfolio referring to a project page located inside another portfolio. To categorize a project in multiple portfolios, copy the project page into each portfolio directory that you want it to appear.

### Example {#portfolio-example}

See rendered page here: ["Portfolio" example](/docs/portfolios-and-pages/example-portfolio/){:target="_new"}
{% coderay source/_example-portfolio/index.markdown %}
---
layout: portfolio_index
title: "Portfolio Example"
projects: [example-design-project, example-app-project]
comments: false
sharing: false
footer: false
---
{% raw %}
## Check out my latest web development projects

Everything below is automatically generated from the projects included in the YAML front matter:
{% endraw %}
{% endcoderay %}

**Tip for Power Users**

Showcase portfolios are built using [Jekyll Collections](http://jekyllrb.com/docs/collections/). By registering a portfolio as a Jekyll Collection, the pages in the portfolio folder becomes accessible to the of **any** Showcase page, i.e. `{% raw %}{% site.portfolio-title %}{% endraw %}` returns a collection of Document objects in `source/_portfolio-title/` folder, much like working with `site.pages` and `site.posts`.

### New Portfolio  
To publish a portfolio to your site, the portfolio must be stored in the `source/` directory, named according to Jekyll's naming conventions: `_portfolio-name/`, and it must be added to the `_config.yml` file in the following format:  

{% coderay _config.yml lang:yaml line_number_start:45 %}
portfolio-name:
  output: true
  permalink: /portfolio-name/:title/
{% endcoderay %}

Additionally, the portfolio name must be added to `source/_data/collections.yml` to make the portfolio available as a menu option in some other rake tasks, e.g. the `new_project` command.

Showcase provides a `new_portfolio` rake task that creates new portfolios with the right naming convention and registers it in all the necessary files for you.

**Syntax**

~~~ bash
$ rake new_portfolio["Portfolio Name"]

# creates /source/_portfolio-name/
# registers "portfolio-name" portfolio in _config.yml
# registers "portfolio-name" portfolio in source/_data/collections.yml
~~~

The `new_portfolio` command expects a naturally written title and will create a url-friendly filename stripped of invalid characters. The default extension for new portfolios is `markdown` though it can be configured in the `Rakefile`.

## Projects
Projects are pre-styled pages that include an image gallery to showcase your work. The gallery is displayed as a slideshow image previewer and filmstrip of thumbnail previews, generated automatically by the configurations provided in the project's [YAML front matter](#anatomy-of-pages).

To publish a project to your site, add the project page to a portfolio directory and add its url-friendly title to `projects:` in the YAML front matter of the portfolio's index page ([see example](#portfolio-example)). 

### Example {#project-example}

See rendered page here: ["Project" example](/docs/portfolios-and-pages/example-portfolio/example-design-project/){:target="_new"}
{% coderay source/_example-portfolio/example-design-project.markdown %}
---
layout: project
title: "Example Design Project"
gallery_path: ../../images/example-design-project/
include_images: [ShowcaseLogo.svg, tobySketch.jpg, elephantigami.png]
cover_image_path: ../../images/example-design-project/ShowcaseLogo.svg
site: 
github:
bitbucket:
---
{% raw %}
^ Everything above is automatically generated by the images included in the YAML front matter. Content appears beneath the image gallery.
{% endraw %}
{% endcoderay %}

### New Project
A project page must be inside a portfolio directory and its url-friendly title must be included in `projects:` list in the [YAML front matter](#anatomy-of-pages) of the portfolio's index page ([see example](#portfolio-example)).

A slideshow image gallery is generated based on the configurations provided in the project's YAML front matter. To include an image in the gallery, its path must be listed in `include_images:` in the project's YAML front matter. (The path is relative to the portfolio directory, or a full url `http://`/`https//` for external images). If the images are stored within a single directory or site url, you can add the path to `gallery_path:` and then include only the image name in `include_images:`.

Showcase provides a rake task that does most of the work for you. The `new_project` command creates a new project with the right naming convention in a target portfolio, creates a project image folder at `source/images/project-name/`, and updates the YAML front matter with the appropriate paths.

**Syntax**

Example 1

~~~ bash
$ rake new_project["portfolio/Project Name"]

# creates a new project page at source/_portfolio/project-name.markdown
# creates a new image folder at source/images/project-name/
~~~

Example 2

~~~ bash
$ rake new_project["Project Name"]
> Portfolios in registry (_data/collections.yml):
> 1 ) _portfolio
> In which portfolio does "Project Name" project belong? (enter number): _

# creates a new project page at source/_portfolio/project-name.markdown
# creates a new image folder at source/images/project-name/
~~~

The `new_project` command expects a naturally written title and will create a url-friendly filename stripped of invalid characters. The default extension for new projects is `markdown` though it can be configured in the `Rakefile`. You can pass in the portfolio directory with the project name to create a project there, or pass only a project name and choose a portfolio when prompted by the command line menu.

## Generate and Preview Site

The `preview` command allows you to preview your site locally as it will appear online when you deploy.

**Syntax**

~~~ bash
$ rake generate # Generates posts and pages into the public directory
$ rake watch # Watches source/ and sass/ for changes and regenerates site
$ rake preview # Mounts a webserver at http://localhost:4000 and watches for changes
~~~


