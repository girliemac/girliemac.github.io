---
title: 'How-to: Migrating Blog from WordPress to Jekyll, and Host on Github'
author: Tomomi Imura
layout: post
categories:
  - Dev
---
![Jekyll on Github](/assets/images/articles/2013/12/jekyll.png "Jekyll on Github")

Last year during holidays, I knitted a <a href="http://www.flickr.com/photos/70561195@N00/8314700407/in/photolist-dEK1Kz-dEK4cT" target="_blank">NyanCat scarf</a>. As this year's project, I finally migrated my Wordpress blog to [Jekyll][jekyll], and host on Github Pages to say good-bye to PHP and web hosting server.

## Why

Wordpress is great, and has been working wonderfully for me. However, I decided to make the change becasue:

1. Jekyll allows [markdown][markdown]. I have been annoyed writing HTML for my blog.
2. The latest Jekyll comes with [Pygment][pygment] syntax highlighter. Writing code snipets is easier in markdown (no need to escape HTML tages, yay!), and the code samples are prettified with Pygment.
3. [Github][gh] offers free hosting, and of course, having version control is awesome.
4. More control using command line is nice. I can use [Grunt][grunt] to automate tasks, including build process and minifying code, too.

[jekyll]: http://jekyllrb.com/ "Jekyll"
[markdown]: http://daringfireball.net/projects/markdown/ "Markdown"
[pygment]: http://pygments.org/ "Pygment"
[gh]: http://pages.github.com/ "Github Pages"
[grunt]: http://gruntjs.com/ "Grunt"

### What I did

While I was migrating, I took notes so I can share with you who wants to do the same.

Here's a list of the steps that I actually went through.

1. Migrate comments on Wordpress to Disqus
2. Export Wordpress contents
3. Install and setup Jekyll
4. Host on Github

I am on Mac OS 10.7.5 (still!), and WordPress 3.7 by the way. Read on if you would like to follow my steps-


## Before leaving WordPress

### Setup Disqus

Skip this process if you're already using Disqus on your WP blog.

First, sign up and register the site with Disqus at [disqus.com/admin/create][disqus].

Go to your WordPress Admin page. Then, go to **Plugins**, serach for **Disqus Comment System plugin** and install it, then activate.

Once activated, check the Disqus Setting to make sure your Disqus account is connected to your WP blog.

![Screenshot](/assets/images/articles/2013/12/wp-disqus.png "screenshot")

To manually migrate the WP comments to Disqus style comments, go to **Tools > Export**, and download the WordPress (WXR) XML file.

![Screenshot](/assets/images/articles/2013/12/wp-export.png "screenshot")

Next, go to [import.disqus.com][discuss-import], upload the xml that you just downloaded from the last step, to import all the comment into Disqus.

![Screenshot](/assets/images/articles/2013/12/disqus-import.png "screenshot")

Go back to your WP Admin page to see if all the comments are available in Disqus plugin.


[disqus]: http://disqus.com/admin/create/
[discuss-import]: http://import.disqus.com

## Leaving WordPress

### Export All WP Contents

Fisrt, install **WordPress to Jekyll Exporter** manually.

   1. Download the zipped source code from the [github][exporter] page.
   2. FTP the upzipped source into the folder in `/wp-content/plugins/`
   3. Activate it in the WP Admin page.

Then go to **Tools > Export to Jekyll** and download a a zip file.

![Screenshot](/assets/images/articles/2013/12/wp-download.png "screenshot")

The exported folder contains all posts and pages that coverted into Markdown. All the images uploaded using WP's *Media Library* are expoted too. If you have images manually uploaded, they may not be included in the zip file.


[exporter]: https://github.com/benbalter/wordpress-to-jekyll-exporter


## Hello, Jekyll!

**Prerequisites**

* [Ruby][ruby]
* [RubyGems][gem]

[ruby]: http://www.ruby-lang.org/en/downloads/
[gem]: http://rubygems.org/pages/download


### Install and setup Jekyll

I am not going to explain how to use **Jekyll** from scratch, so please go to [Jekyll][jekyll]'s official site to learn the ABC, if you are not already familiar.

Install jekyll ruby gem locally, and create a new Jekyll blog:

```bash
$ gem install jekyll
$ jekyll new yourname.github.io
```

Where `yourname.github.io`, I named mine `girliemac.github.io`. By naming the github repo with this format, you can serve up your blog on the url, `http://username.github.io`, although you can use your own domain name.

This gives you a clean Jekyll site and no fluff.
![Screenshot](/assets/images/articles/2013/12/jekyll-new.png "screenshot")

Alternatively, you can use some pre-designed templates. Go to [jekyllthemes.org][theme], and download one.


[theme]: http://jekyllthemes.org/

### Import the WP Contents

Unzip the `jekyll-export.zip` you exported off your WordPress. The `_post` filder should contain all blog posts in markdown, and `wp_content` has images. Other static pages should have its own folder as well.

Copy them into your new `yourname.github.io` (or whatever you named) folder.
You may want to manually tweak the  `_config.yml` file, or merge the exported `_config.yml` file with the one comes with the theme you downloaded, rather than just overwriting.

To use the *Pygments* syntax highlighter, add this line in your  `_config.yml`.

```bash
pygments: true
```

Once everything is ported into the new jekyll project folder, build the site and preview on browser.

To build,

```bash
$ cd yourname.github.io
$ jekyll build
```

The current folder will be generated into `./_site`

To view the generated site locally,

```bash
$ jekyll serve
```
By default, your development server runs at `http://localhost:4000/`.

## Add Disqus Comments

To include Disqus comments and the legacy comments ported from old WordPress is easy.

Login on Disqus, and copy the *Universal Embed Code* from [Disqus][embed]. (Once logged in, the `disqus_shortname` should be already generated for you. Otherwise, add it manually.)

Paste the code into where you want the comments to be displayed in `_layouts/post.html`.

Once you deploy, the Disqus comment form along with the old commnets should be appeared on the new blog!

[embed]: http://docs.disqus.com/developers/universal/


## Optional: Use Grunt

**Prerequisites**

* [Node.js][node]
* grunt-cli<br>
```
$ sudo npm install -g grunt-cli
```

[node]: http://nodejs.org/

Grunt is a JavaScript tast runner that you can automate some repetitive tasks.

Useful grunt plugins for Jekyll can be:

* `grunt-contrib-jshint` jsHint
* `grunt-contrib-cssmin` to minify CSS
* `grunt-contrib-uglify` to minify JavaScript
* `grunt-contrib-imagemin` to optimize images
* `grunt-shell-spawn` to include `jekyll build` command
* `grunt-contrib-watch` to monitor if specified files are modified run tasks
etc.

For more information, go to [gruntjs.com][grunt].

## Deploy to Github Pages

So long, my web server, I port everything on my github for free!

Some files and directries don't need to be pushed to github. Put `_sites` and `node_modules` if using Grunt in `.gitignore` file. (and of course, `.DS_Store` if you are a Mac user! ugh!)

Commit and push your Jekyll site to github. You don't need to create a `gh-pages` branch, when you name the repo with `yourname.github.io`.

## Set a Custom Domain Name

### Set a CNAME on Github

1. Create a file named `CNAME`
2. in the file, put your domain name, without `http://`. In my case:

```
girliemac.com
```


### Set up DNS

Basically, all you need is to set these.

**A Record**: 204.232.175.78<br>
**CNAME**: yourname.github.io

I use NameCheap.com to manage my domain names, and this is a screenshot of the host setup on namecheap.com. Your registrar probably has a similar setting.

![Screenshot](/assets/images/articles/2013/12/domain-namecheap.png "screenshot")

If you don't see the "All Host Records" link, you probably need to disconnect from your previous web host DNS by clicking "Transfer the DNS back to us") and follow the instruction first.
This takes about a few hours to complete.


Ta-da! Now I have my blog ported on github!
