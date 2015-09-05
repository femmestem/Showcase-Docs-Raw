---
layout: page
title: "Blogging"
comments: false
sharing: false
footer: false
sidebar: false
---
Showcase includes rake tasks to create posts preloaded with metadata. It also generates a global and a category-based feed for your posts (which you can find in `atom.xml` and `blog/categories/<category>/atom.xml`).

**Note:** If you are using zsh in the command line, then add `alias rake=noglob rake` to your zsh config to prevent the `zsh: no matches found` error that occurs when running these rake tasks.

Some command line interpreters, e.g. zsh, have a special meaning for `[` and `]`. For rake tasks with options `$ rake task_name[option]`, you have to escape the brackets or temporarily switch to bash.


Go to:  
[Anatomy of Posts](#anatomy-of-posts)  
[Draft Posts](#draft-posts)  
[Published Posts](#published-posts)  
[Publish and Unpublish Posts](#publish-and-unpublish-posts)  
[Generate and Preview Site](#generate-and-preview-site)  

## Anatomy of Posts  
{% assign openTag = '{%' %}  
Each post must include YAML front matter at the top (the content between two fences `---`) which tells Jekyll how to process files. Attributes in the front matter can be accessed dynamically within the content area using Liquid templating language, e.g. `{% raw %}{% page.attributeName %}{% endraw %}`.

Below the front matter is the content area. Anything in the content area will appear on the page. By default, posts and pages are markdown files, which accept any combination of markdown syntax, plain text (interpreted as Markdown), HTML, and Liquid templating syntax.

To prevent a block of text from being parsed by the markdown preprocessor so that it appears as-is, enclose it between `{{ openTag }}{% raw %} raw %}{% endraw %}` and `{{ openTag }}{% raw %} endraw %}`{% endraw %} tags.

To keep comment text hidden from the rendered page, include it between `{% raw %}{% comment %}{% endraw %}` and `{% raw %}{% endcomment %}{% endraw %}` tags.

**Example**

See rendered page here: ["Anatomy of Posts" example](blogging/anatomy-of-posts/){:target="_new"}
{% coderay source/_posts/anatomy-of-posts.markdown %}
---
layout: post
date: 2015-08-01 08:10:07 -0700
title: "Anatomy of Posts"
comments: true
sharing: false
categories: [demo, markdown, embedded code]
---
{% raw %}
<h2> Anything Written Here Is Page Content </h2>
{% comment %}This text won't be rendered when you build the site.{% endcomment %}

<strong>This</strong> will render the same as **that**.

### You Can Render the Page's YAML Front Matter with Liquid

Page Title: {{ page.title }}    
Categories: 
{% for category in page.categories %}"{{ category }}" {% endfor %}

### You Can Embed Code Snippets

    ```
    def sayhello
        puts "Hello World!"
    end
    ```

...with syntax highlighting

    ```ruby
    def sayhello
        puts "Hello World!"
    end
    ```

...and downloadable code snippets:

{% codeblock helloworld.rb http://mysite.com/helloworld.rb Download %}
    def sayhello
        puts "Hello World!"
    end
{% endcodeblock %}

{% endraw %}
{% endcoderay %}

## Draft Posts
Draft posts are stored in the `source/_drafts` directory, which allows you to work on blog posts without including them in the site build. Draft posts will also be hidden by default when you preview the site locally with the `preview` command. To preview the site with both published posts and drafts you must use `preview[drafts]`. 

### New Draft
Showcase provides a rake task to create new drafts with the right naming convention.

**Syntax**

~~~ bash
$ rake new_draft["Post Title"]
~~~

The `new_draft` command expects a naturally written title and will create a url-friendly filename stripped of invalid characters. The default extension for new draft posts is `markdown` though it can be configured in the `Rakefile`.

**Example**

~~~ bash
$ rake new_draft["Learn Command Line the Hard Way"]
# creates /source/_drafts/learn-command-line-the-hard-way.markdown
~~~

A freshly generated page will look like this:

{% coderay source/_drafts/learn-command-line-the-hard-way.markdown %}
---
layout: post
title: "Learn Command Line the Hard Way"
comments: true
categories: []
---

{% endcoderay %}

## Published Posts
To publish posts to your site, the post must be stored in the `source/_posts` directory and named according to Jekyll's naming conventions: `YYYY-MM-DD-post-title.markdown`. The name of the file will be used as the url. The date helps with file distinction and determines the sorting order.

Showcase provides a rake task to create new blog posts with the right naming convention.

**Syntax**

~~~ bash
$ rake new_post["Post Title"]
~~~

The `new_post` command expects a naturally written title and will create a url-friendly filename stripped of invalid characters and prepended with a datestamp. The default extension for new posts is `markdown` though it can be configured in the `Rakefile`.

**Example**

~~~ bash
$ rake new_post["Learn Command Line the Hard Way"]
# creates /source/_posts/learn-command-line-the-hard-way.markdown
~~~

A freshly generated page will look like this:

{% coderay source/_posts/learn-command-line-the-hard-way.markdown %}
---
layout: post
date: 2015-08-01 08:30:12 -0700
title: "Learn Command Line the Hard Way"
comments: true
categories: []
---

{% endcoderay %}

## Publish and Unpublish Posts

### Publish Draft

Drafts can be converted to posts, which will be included in the site build when you deploy to the live site, using the `publish` command. This moves the post from `source/_drafts` to `source/_posts` and adds a datestamp to the filename and yaml front matter.

**Syntax**

Example 1

~~~ bash
$ rake publish["post-title.markdown"]
~~~

Example 2

~~~ bash
$ rake publish
>> Drafts waiting to be published:
>> 1 ) post-title.markdown
>> 2 ) other-post-title.markdown
>> Enter menu number(s) of file(s) to update: _
# You can enter multiple items to be unpublished
~~~

### Revert Post to Draft

Posts that have been published can be reverted to draft mode using the `unpublish` command. This moves the post from `source/_posts` to `source/_drafts` and strips the post of its datestamp in the filename and yaml front matter.

**Syntax**

Example 1

~~~ bash
$ rake unpublish["2015-08-01-post-title.markdown"]
~~~

Example 2

~~~ bash
$ rake unpublish
>> Published posts:
>> 1 ) 2015-08-01-post-title.markdown
>> 2 ) 2015-08-05-other-post-title.markdown
>> Enter menu number(s) of file(s) to update: _
# You can enter multiple items to be unpublished
~~~

## Generate and Preview Site

~~~ bash
$ rake generate    # Generates posts and pages into the public directory
$ rake watch       # Watches source/ and sass/ for changes and regenerates site
$ rake preview     # Mounts a webserver at http://localhost:4000 and watches for changes
~~~

The `preview` command allows you to preview your site locally as it will appear online (that is, without drafts). You can also pass the `drafts` option to preview the site with draft posts (though they will stil be excluded when generating the actual site).

**Show Published Posts Only**

~~~ bash
$ rake preview
~~~

**Show Posts and Drafts**

~~~ bash
$ rake preview[drafts]
~~~




