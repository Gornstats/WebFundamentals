Web Fundamentals
================

Web Fundamentals is a technical documentation center for multi-device web 
development.  Our goal is to build a resource for modern web developers 
that’s as curated and thorough as developer.android.com or iOS Dev Center.


Content plan
------------
Content plan for Web Fundamentals is tracked through GitHub Issues and our [Site Structure + Content Inventory](http://goo.gl/nWDD0M) doc


Release status
--------------

The project was soft launched in late April with a formal v1 launch in June 2014.  We've now moved to a six-week rolling release cycle.

Technology
----------

This is a Jekyll build.

```
/src
  /appengine - the server to host the static content
  /site - the documentation
    /_en/ - the base language folder
      /getting-started - the getting started articles
      /multi-device-layouts - responsive design guide
      /introduction-to-media - the guide to using media
      /optimizing-performance - the perf articles
      /using-touch - managing touch
      /showcase - the case-studies
    /_langcode/ - overrides for that language, following the main path structure.
```

`/build` is never checked in but generated by Jekyll.


Contributing
------------

Web Fundamentals is an open source project and we welcome your contributions! 
Before submitting a pull request, please review [CONTRIBUTING.md](CONTRIBUTING.md)
and make sure that there is an issue filed describing the fix or new content.
If you don't complete these steps, we won't be able to accept your pull request, sorry.


Installing Dependencies
=======================

Mac
---

1. Install [XCode Command Line Tools](https://developer.apple.com/xcode/downloads/)
1. Install [RVM](https://rvm.io/rubies/default)
    * `curl -sSL https://get.rvm.io | bash`
1. Set RVM Default to 2.0.0
    * `rvm install ruby-2.0.0-p451`
    * `rvm --default use 2.0.0`
1. Install [Pygments](http://pygments.org/)
    * `easy_install pygments`
1. Install [RubyGems](https://rubygems.org/) dependencies ([Jekyll](http://jekyllrb.com/), [Kramdown](http://kramdown.gettalong.org/) and [Sass](http://sass-lang.com/install)) 
    * cd src/ && `bundle install`
1. Install [Node.js](http://nodejs.org/)
1. Install the [Grunt CLI](http://gruntjs.com/)
    * `npm install -g grunt-cli`

Running the site
================

Once you have all the dependencies installed go to the root of the checked out repo and type:

```
make server
```

This will have Jekyll build the site, run a static server to listen on port 8081 (which you can now reach at http://localhost:8081/web/fundamentals/), and watch for changes to site files. Every change will cause Jekyll to rebuild the affected files.


Using project-level meta data
=============================

The table of contents is generated from `src/site/_project.yaml`

To parse the `_project.yaml` file, include `{% injectdata content _project.yaml %}` in the page. You then have access to the variables in the page object.


Generating Table of Contents
----------------------------

The table of contents is generated from `src/site/_book.yaml`

To parse the `_book.yaml` file, include `{% injectdata content _book.yaml %}` in the page and then iterate as follows:

     {% for section in page.content.toc %}
        SOME MARKUP
     {% endfor %}

Jekyll Special elements
-----------------------

* Code import: `{% highlight javascript %} {% include sample1.js %} {% endhighlight %}`
* `{{ articles _category_}}` a list of articles in divs, ordered by the "order" preamble.
* `{{ showcases _category_}}` a list of showcases.


Translations
=============================

The base content is in english under the "_en" directory. Translations can be added following the same structure with either a two letter or composite language code: e.g. "_es", "_pt-br". 

To test translations set the lang variabe in the _config.yml. For example, to set the mode to French:

    lang: "fr"

Note the underscore is not required here. 

To ensure the content is built when being released onto developers.google.com, ensure that the langs_available list in _config-devsite.yml is updated to include any new language directories being added. For example, to add French:

    langs_available: ["fr"]
