Articles on girliemac.com are in Markdown. [Jekyll][jekyll] is used to generate the static HTML for the site, and the output is generated into a `_site` folder and served from Github pages.

## Prereqs and installation requirements

We use Jekyll 1.4.2+ and [Grunt][grunt] to automate some tasks. 

```bash
$ gem install jekyll
$ npm install -g grunt-cli
```

**Note:** If you receive permission warnings, you may need to run the above tasks with `sudo`.


Run `npm install` to pull down dependencies. 


## Editing and creating new articles


Jekyll generates the static site in a folder named `_site`. 
Once done, `git commit` them and push to master (no gh-pages) and Github builds the jekyll automatically.



[jekyll]: http://jekyllrb.com/
[grunt]: http://gruntjs.com/
