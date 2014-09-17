---
layout: post
title: "How to build this blog - Part 1"
date: 2014-09-15 13:19:42 +0700
comments: true
categories: [Tutorials]
tags: [jekyll, octopres, bootstrap3, octostrap3, github, gh-page]
---

>It's been a month since I knew about GitHub Page and Jekyll - 2 terrific  things which powered this blog. But until last week, I've just figured out [Octopress](http://octopress.org/) - A blogging framework for hackers - which is on top of jekyll.It helps making the simple blog never easier. And one of the most awesome thing that they are all free ! So in this tutorial, I'll guide you step-to-step to build a simple blog like mine.

First of all, we need to install and config a lot, I'll try to make it simple.
<h3>Jekyll Installation</h3>
Jekyll is a static site generator - more on [Jekyllrb](http://jekyllrb.com/docs/home/). [GitHub Pages](https://pages.github.com/) uses it, so everything you write in Jekyll will easily host on Github. 
<h4>Requirements</h4>
* [**Ruby >= 1.9**](http://www.ruby-lang.org/en/downloads/) - Read [this](https://gorails.com/setup) if you don't have Ruby installed   
* [**RubyGems**](http://rubygems.org/pages/download)
* **Linux, Unix or MacOS** 
<h4>Install via RubyGem</h4>
``` sh ~/
$ gem install jekyll
```
**Now you can easily start your site by**

``` sh ~/
$ jekyll new my-blog
$ cd my-blog
my-blog$ jekyll serve 
# => Now browse to http://localhost:4000
```
By browsing above address you can see your beautifully simplified site now there. 

#### Early Deployment to Github Page

* Sign in into your GitHub account, create [one](https://github.com/) if you don't have
* Create a new repository with name like **username.github.io**
* E.g., my repo for this blog is ``rexey3s.github.io``
* Now back to your console and make sure you have Git installed

``` sh ~/
$sudo apt-get install git
$cd my-blog
my-blog$ git init 
my-blog$ git add .
my-blog$ git commit -m 'Deloying my Jekyll Blog'
my-blog$ git remote add origin https://github.com/<username>/<username>.github.io
my-blog$ git push origin master
```
Go to your browser and pointing to **username.github.io**, as you can see your blog is now online without any 3rd party host.

If you want to build your site from scratch, you can carefully read the [docs](http://jekyllrb.com/docs/usage/) and again deloy it to GitHub Page. There are many options to deploy a Jekyll site, GitHub Page is just a free and great one. But if you want a quick and easy customizable site then continue reading.

### Octopress Installation
**Setup Octopress**

``` sh ~/
$ mkdir myblog
$ git clone git://github.com/imathis/octopress.git myblog
$ cd myblog
```

**Install dependencies**

``` sh ~/myblog/
myblog$ gem install bundler
myblog$ bundle install
```

**Install Octopress** - Choose your [themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes) 

``` sh ~/myblog/
myblog$ git submodule add GIT_THEME_URL .themes/THEME_NAME
myblog$ rake install['THEME_NAME']
myblog$ rake generate
# => Now browse to http://localhost:4000
```

#### Octopress config

**_config.yml** - Jekyll main config file 

``` sh ~/myblog/
myblog$ vim _config.yml
# ----------------------- #
#      Main Configs       #
# ----------------------- #
url: http://<username>.github.io
title: "put your blog title here"
subtitle: A blogging framework for hackers.
author: me
description:
date_format:        # Format dates using Ruby's date strftime syntax
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
```

Note: After changing any configs in **_config.yml**, you have to type ``rake generate`` again to take effect

**Octopress bundled with a lot 3rd Party setting setting**

``` sh ~/myblog/
myblog$ vim _config.yml
# ----------------------- #
#   3rd Party Settings    #
# ----------------------- #
# Github
github_user: YOUR_GITHUB
# Twitter
twitter_user: YOUR_TWTTTER_NAME
twitter_tweet_button: true
# Disqus Comments
disqus_short_name: DISQUS_NAME
disqus_show_comment_count: false
# Facebook Like
facebook_like: false
```

_Comments powered by Disqus - signup [one](https://disqus.com) if you don't have_

**Learn more about [Octopress config](http://octopress.org/docs/configuring/)**

### Customize your blog

#### Changing default theme

This blog uses [Octostrap3](https://github.com/kAworu/octostrap3) and [Bootwatch Readable](http://bootswatch.com/readable/)

``` sh ~/myblog/
~/myblog$ git clone https://github.com/kAworu/octostrap3 .themes/octostrap3
~/myblog$ rake install[octostrap3]
~/myblog$ rake generate
```

Go to [Bootwatch](http://bootswatch.com/) and choose the theme you like, then copy ``bootstrap.min.css`` 's content and replace your ``myblog/source/assets/bootstrap/dist/css/bootstrap-theme.min.css``  by its content. **Refresh your browser** at [localhost:4000/](http://localhost:4000/) and check out the new look.

### Create About page 

**About page**

``` html source/about/index.html
---
layout: page
title: "About"
footer: true
navbar: About
---
<div class="row">
  <div class="col-xs-8 col-md-3">
    <a href="#" class="thumbnail">  
    <img src="/images/bio-photo-alt.jpg" title="Avatar" />
    </a>
  </div>
  <div class="col-xs-8 col-md-5">
    <p>Write about you</p>
  </div>
</div>
```

Then navigate to ``source/_includes/custom/navigation.html`` add the following snippet to inside ``div.navbar-collapse`` tag


``` html ~/myblog/source/_includes/custom/navigation.html
<li>
    <a href="/about/">About</a>
</li>
```

### Deploy to GitHub pages

Now, you don't need to run ``git`` anymore ``rake deploy`` will do it for you 

``` sh ~/myblog/
myblog$ rake preview
myblog$ # => take a look at your blog on http://localhost:4000 before were deploy it
myblog$ rake setup_github_pages
```

The ``rake`` task will ask you for a URL of your Github Repo which can be one of 2 following forms:

* ``git@github.com:username/username.github.io.git``
* ``https://github.com/username/username.github.io``

**Deploy**

``` sh ~/myblog/
myblog$ rake generate
myblog$ rake deploy # You will be prompted for Github username and password
```

Now go to ``username.github.io`` and see your result. 

One more important thing is to backup your Octopress's code to Github too. In ``~/myblog/`` dir ``init`` a new git to push your source to a repo that would store your Octopress's code. Note: You may not want to public your ``_config.yml`` file just add it to ``.gitignore``

``` sh ~/myblog/
myblog$ git init 
myblog$ git remote add origin https://github.com/username/blog-src.git
myblog$ git add .
myblog$ git commit -m 'Backup src to 'source' branch'
myblog$ git push origin master
```

Great, now your blog has been online, hosted by Github Page which is free of charge and also your source code has been subversioned by Github. There are more interesting stuffs about Octopress that I will see you in the next part.

Here some helpful links:

 * [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) - the language
 * [Octopress Docs](http://opress.org/docs)
 * [Bootwatch](http://bootswatch.com) - Bootstrap's Themes