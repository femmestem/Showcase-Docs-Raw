---
layout: page
title: "Anatomy of Pages"
permalink: /docs/portfolios-and-projects/anatomy-of-pages/
comments: false
sharing: false
footer: false
---
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
