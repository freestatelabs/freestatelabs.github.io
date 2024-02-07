# README

This repository contains the Markdown files, assets, and other Jekyll input data for the freestatelabs github.io website. 

Contact: ryan@freestatelabs.com

## Development Notes

See [here](https://medium.com/@ritviknag/ruby-versioning-trouble-with-jekyll-github-pages-fd2748bf4e1d) 
and [here](https://thoughtfulapps.com/articles/jekyll/ruby/undefined-method-tainted-jekyll-error) for resolving
Ruby/Bundle/Jekyll/Liquid dependency issues.  

TLDR: 
```
$ brew install rbenv 
$ rbenv install 3.1.3 
$ rbenv global 3.1.3 
$ gem install bundler 
$ bundle install                # will downgrade to Bundler 2.3.15 
$ bundle exec jekyll serve      # fingers crossed, it should work now...
```