---
layout: post
title:  "Bootstrapping Jekyll"
date:   2018-09-02 15:39:36 -0700
categories: jekyll tech
---

Jekyll has official installation instructions [here](https://jekyllrb.com/docs/installation/). For those of us
who already have a ruby environment set up, this suffices:


```
$ gem install bundler jekyll
```

This installs `jekyll` itself, which is a static site generator. `bundler` helps ruby projects
to be more universally runnable by managing dependencies. To see this, let's invoke jekyll and
produce the base site template:

```
$ jekyll new site  # makes a directory called 'site' with stuff inside it
$ cd site
$ ls
404.html  Gemfile  Gemfile.lock  _config.yml  _posts/  _site/  about.md  index.md
$ bundler show
Gems included by the bundle:
  * addressable (2.5.2)
  * bundler (1.16.4)
  * colorator (1.1.0)
  * concurrent-ruby (1.0.5)
  * em-websocket (0.5.1)
  * eventmachine (1.2.7)
  * ffi (1.9.25)
  * forwardable-extended (2.6.0)
  * http_parser.rb (0.6.0)
  * i18n (0.9.5)
  * jekyll (3.8.3)
  * jekyll-feed (0.10.0)
  * jekyll-sass-converter (1.5.2)
  * jekyll-seo-tag (2.5.0)
  * jekyll-watch (2.0.0)
  * kramdown (1.17.0)
  * liquid (4.0.0)
  * listen (3.1.5)
  * mercenary (0.3.6)
  * minima (2.5.0)
  * pathutil (0.16.1)
  * public_suffix (3.0.3)
  * rb-fsevent (0.10.3)
  * rb-inotify (0.9.10)
  * rouge (3.2.1)
  * ruby_dep (1.5.0)
  * safe_yaml (1.0.4)
  * sass (3.5.7)
  * sass-listen (4.0.0)
```

Running `bundler exec jekyll serve` in this directory runs this project's version of jekyll (currently 3.8.3)
with the "serve" subcommand. This will hotload your templated website. Success!

<table><tr><td>
    <img src="/assets/img/jekyll-minima.png" />
</td></tr></table>

Add files to the `_posts` directory and voila, you have a blog. `jekyll serve` will help you develop it, and
`jekyll build` will generate a `_site` directory, the contents of which are deployable to any web server.

# Looking under the hood

One of the strengths of jekyll is that it comes with [a lot of themes](https://github.com/mattvh/jekyllthemes). 
At the time of this writing, `minima` is the one that comes with jekyll by default. You might find that
a theme is _almost_ what you want, but it needs some tweaking. So how do we do that? Well, let's take
a look at minima's contents.

```
$ bundle show minima
/usr/local/lib/ruby/gems/2.5.0/gems/minima-2.5.0
$ ls /usr/local/lib/ruby/gems/2.5.0/gems/minima-2.5.0
LICENSE.txt  README.md  _includes/  _layouts/  _sass/  assets/
```

These are the folders described in [the jekyll docs](https://jekyllrb.com/docs/pages/). So when you set a
jekyll theme, you're inheriting these contents from the theme. Each of these folders can be "extended"
by putting a folder with the same name in your site.

Another option is to just copy the theme locally. This reduces your dependencies and also gives you
more control.

```
$ SITE=`pwd`
$ cd `bundle show minima`
$ cp -r _includes  _layouts  _sass  assets $SITE
$ cd $SITE
```
