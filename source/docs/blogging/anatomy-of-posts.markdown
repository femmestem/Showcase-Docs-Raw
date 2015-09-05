---
layout: post
date: 2015-08-01 08:10:07 -0700
title: "Anatomy of Posts"
comments: true
sharing: false
categories: [demo, markdown, embedded code]
permalink: /docs/blogging/anatomy-of-posts/
---
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
