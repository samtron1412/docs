[TOC]

# Overview

# GitHub Pages

## Creating a GitHub Page

- Type of pages
    + Personal and organization
    + Project
- Personal and organization
    + Create a repository with the name: `<username>.github.io`
    + Put your website's code there
- Project
    + Create a new branch in your project: `gh-pages`
        * `git checkout --orphan gh-pages`: create an empty branch
    + Put your website's code in there

## Jekyll and GitHub Page

- Install Ruby
    + `brew install ruby`
    + Add ruby path into your ~/.bashrc file
        * `export PATH=/usr/local/opt/ruby/bin:$PATH`
    + Add ruby gems path into your ~/.bashrc file
        * Check your ruby version: `ruby -v`
        * `export PATH=$HOME/.gem/ruby/X.X.0/bin:$PATH`
        * Replace `X.X` with your ruby version, e.g. 2.6
- Install Bundler and Jekyll
    + `gem install --user-install bundler jekyll`
- cd to your GitHub repository of the page and run: `bundle install`
    + This command will install all the ruby gems needed for the site
- Make changes to your site
- Build your site
    + `bundle exec jekyll serve`
- View your site at `http://localhost:4000`
- How to add a favicon?
    + https://medium.com/@xiang_zhou/how-to-add-a-favicon-to-your-jekyll-site-2ac2179cc2ed


# Tips and Tricks

## Get all files url in a repository

https://stackoverflow.com/questions/25022016/get-all-file-names-from-a-github-repo-through-the-github-api

# References

[api]: https://developer.github.com/v3/
[hub - cli interface for Github]: https://github.com/github/hub
[Github command line]: https://github.com/defunkt/github-gem
[Emoticon on GitHub commit messages]: https://scotch.io/bar-talk/emoji-icons-in-github-commit-messages
[GitHub ranking]: https://github-ranking.com/
