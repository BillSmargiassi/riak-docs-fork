# Required tasks to host `basho_docs`

The `basho_docs` repo is set up to live at docs.basho.com. That made sense at one point, but it no longer does. The `relocatable` branch is meant to make it a little easier to move to a new location and drop some links to basho.com.

## Site name

In the `config.yaml` file `baseURL` sets the location of the docs site. It’s likely that not every set of docs will want to dedicate an entire host name to the docs site. I have set `canonifyurls` to true so that the whole site can be hosted in a sub-directory an arbitrary amount of levels deep from the root level of the host.

## Google Custom Search engine

The search field uses Google [Custom Search Engine][1]. Google will return results for a particular site after it’s crawled the site. You’ll have to set up CSE and put the code it generates into `layouts/partials/google-search.html` or else it will send search results to the last site configured.

## Robots.txt setup

This is one exception to the `canonifyurls` setting. You’ll need to move `robots.txt` from any subdirectory, because it needs to reside at the top level of the site. You’ll need to alter any paths in it to add the extra level of subdirectories and then copy it to the top of the site after you use Hugo to deploy the site.

## Deploying the site

As usual with [Hugo][2], you run the command `hugo` to generate the Markdown into an HTML site you can deploy. If you are running Hugo on the web server host, use the `-d` switch to point where to build the site. Otherwise, run `hugo` on it’s own, and then use `rsync -a` to copy the files from `public/` to the location on the other host.

You can use `hugo server` to run the site in development mode, but the Riak docs site won’t run on a system with less than 2GB available.

[1]:	https://www.google.com/cse/
[2]:	http://gohugo.io/