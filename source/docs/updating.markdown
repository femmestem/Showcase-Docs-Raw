---
layout: page
title: "Updating Showcase"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/updating/
---
## How to Update

~~~bash
$ git pull showcase master      # Get the latest version of Showcase
$ bundle install                # Keep gems updated
$ rake update_source            # Update the template's source
$ rake update_style             # Update the template's style
~~~

This will update your plugins, theme, gemfiles, rakefile and configs, while preserving your custom pages, blog posts, and styles. Read on for an explanation of how all this works.

### How Updating Works

In the open source world, version control generally takes care of staying current with the latest releases, but once you've begun to customize your code, merging in updates isn't always what you want. So, here is how changes are handled by Showcase:

Plugins, configs, gemfiles, .themes, .gitignore and the Rakefile are all tracked for easy to updating and collaborating.

The install process copies layouts, pages, javascripts, and styles out of the `.themes/` directory. Once you've installed a theme, none of the files under source or sass are in any repository except your own. This way, you can change them to your liking without worrying about merging in updates that blow away your changes.

When you pull down changes from the Showcase repository, the latest layouts, pages, javascripts and styles are merged into your `.themes/` directory. To update your site, you must manually merge in the new files. Showcase comes with some Rake tasks to help out with this.

### Updating Templates with Styles

Update your `source/` and `sass/` directories with a single command.

~~~bash
$ rake update
~~~

This will run `update_style` and `update_source`. You can run these independently if you only want to update one part of your project (see below).

### Updating the Template Source

If you've pulled in changes and you want to update your `/source` directory, run

~~~bash
$ rake update_source
~~~

This task will:

1. Move `source/` to `source.old/`
2. Copy `.themes/classic/source/` to `source/`
3. Copy back everything in `source.old/` (cp -rn - without replacing )
4. Replace everything in `/source/_includes/custom/` with `source/.old/_includes/custom/`, which includes head, header, navigation, footer and custom asides.

This way, all of the files you've added, eg. `_posts/`, `about.html`, etc., and all the customizations in `source/_includes/custom/` will be preserved while all files tracked by Showcase will be updated. If you made changes elsewhere, you can copy them back them from `source.old/` or check them out from your git repository. After you have the update in place, you can remove the `source.old/` directory.

### Updating the Template Styles

If you've pulled in changes and you want to update your `sass/` directory, run

~~~bash
$ rake update_style
~~~

This task will:

1. Move `sass/` to `sass.old/`
2. Copy `.themes/classic/sass/` to `sass/`
3. Replace `/sass/custom/` with `/sass.old/custom/`

This way, if you keep your theme changes in `/sass/custom/` you'll be able to upgrade your stylesheets without losing any of your work. If you made changes elsewhere, you can manually copy them back them from `sass.old/`. After you have the update in place, you can remove the `sass.old/` directory.

<br><br>
Credit: [Brandon Mathis](https://github.com/imathis/)
