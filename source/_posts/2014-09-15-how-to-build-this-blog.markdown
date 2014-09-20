---
layout: post
title: "How to build your blog with Octopress - Part 1"
date: 2014-09-15 13:19:42 +0700
comments: true
categories: [Tutorials, Octopress]
contents: [Introduction, Jekyll Installation, Octopress Installation, Customize your blog, Deploy to GitHub pages, Create a new post]
tags: [jekyll, octopress, bootstrap3, octostrap3, github, github-page]
---

### Introduction

>It's been a month since I knew about GitHub Page and Jekyll - 2 terrific  things which powered this blog. But until last week, I've just figured out [Octopress](http://octopress.org/) - a blogging framework for hackers - which is framework that helps making your pesonal blog or site become easier. And one of the most important reason that I love them is they are all free!

>In this tutorial, I'll show you how to build a blog using Octopress. If you have already known about Jekyll, I suggest you should take a look on Octopress. Unless you have, you don't need to know much about Jekyll because Octopress will handle it for you.    

First of all, we need to install and config a lot,but  I'll try to make it simple.

### Jekyll Installation 

To whom still don't know, [Jekyll](http://jekyllrb.com/docs/home/) is a static site generator which helps you generate your site's or blog's contents ( usually written in Markdown) into static contents (e.g., html, css and javascript). In addition, [GitHub Pages](https://pages.github.com/) have been using [Jekyll](http://jekyllrb.com/) as their pages generator , so everything you write in Jekyll will easily host on Github.

#### Requirements

* [**Ruby >= 1.9**](http://www.ruby-lang.org/en/downloads/) - Read [this](https://gorails.com/setup) if you don't have Ruby installed   
* [**RubyGems**](http://rubygems.org/pages/download)
* **Linux, Unix or MacOS** 

#### Install via RubyGem

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

If you want to build your site from scratch, you can carefully read the [docs](http://jekyllrb.com/docs/usage/) and again deloy it to GitHub Page. There are many options to deploy a Jekyll site, GitHub Page is just a free and awesome one. But if you want a quick and easy customizable site then continue reading.

### Octopress Installation

#### Setup Octopress

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
```
``` vim _config.yml
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

#### Create About page 

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
    <p>Write something about you</p>
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

**Deploying**

``` sh ~/myblog/
myblog$ rake generate
myblog$ rake deploy # You will be prompted for Github username and password
```

Now go to ``username.github.io`` and see your result. 

One more important thing is to backup your Octopress's code to Github too. In ``~/myblog/`` dir, ``init`` a new git to push your source to a repo that would store your Octopress's code. Note: You may not want to public your ``_config.yml`` file, then you can add it to ``.gitignore``

``` sh ~/myblog/
myblog$ git init 
myblog$ git remote add origin https://github.com/username/blog-src.git
myblog$ git add .
myblog$ git commit -m 'Backup src to 'source' branch'
myblog$ git push origin master
```

Great, now your blog has been online, hosted by Github Page which is free of charge and also your source code has been subversioned by Github.

Last but not least, I have to mention that your posts should been written in [Markdown](https://help.github.com/articles/markdown-basics) which allows you to write using an easy-to-read, easy-to-write plain text format, which then converts to valid HTML for viewing on GitHub or anywhere that has a Markdown Conversion Tool. I pretty sure that you will find it easier than writting you own HTML ;). Here is an example to illustrate my words:

I have a code snippet

``` sh Code snippet example
$ jekyll serve
```

If I wrote it in HTML, it would be like this:

``` html HTML elements of Code snippet example
<div class="bogus-wrapper">
 <notextile>
  <figure class="code">
   <figcaption>
    <span>Code snippet example</span>
   </figcaption>
   <div class="highlight">
    <table>
     <tbody><tr>
      <td class="gutter">
        <pre class="line-numbers">
         <span class="line-number">1</span>
        </pre>
      </td>
      <td class="code">
       <pre>
         <code class="sh">
          <span class="line"><span class="nv">$ </span>jekyll serve</span>
         </code>
        </pre>
      </td>
     </tr>
    </tbody>
    </table>
   </div>
 </figure>
 </notextile>
</div>

```

Then I wrote it in Markdown, which would be easily generated to the HTML above

```
 ```sh Code snippet example
 $ jekyll serve
 ```
```

As you have seen, ```  is a syntax for code snippet and  **sh** is specified the language that it would syntax highlighted for - is this example, It is **bash/shell**. Markdown syntax is just beautiful and simplified.

### Create a new post

```sh ~/myblog/
myblog$ rake new_post["this_is_the_title"]
```

Then, go to ``myblog/source/_posts/`` to edit your new post, you can use any editor you like to write it in Markdown syntax. **Note**: the filename of your post would be in the following form

* ``year-month-day-title.md`` - you should not change its ``date`` prefix.

So now you would be able to deploy your site online and create a new post.  Please take a look at Markdown syntax link below, it will help you a lot when writing your post. Happy blogging! 

Here are some helpful links:

 * [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) - The language syntax
 * [Octopress Docs](http://opress.org/docs)
 * [Bootwatch](http://bootswatch.com) - Bootstrap's Themes

>There are still a lot interesting stuffs about Octopress that I would like to show you in the next part of this tutorial. See ya! Thank you for reading my post.

