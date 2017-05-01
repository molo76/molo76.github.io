---
layout: post
title: "Run Jekyll Locally"
date: 2017-04-30
---
Rather than editing this site directly on github through the web front end, I have been using command-line git to clone the repository to my laptop, edit files, then commit and push back to github. It works well but every small edit requires a push into the repository to see the results, good or bad. It becomes a bit time consuming, but does up your github commit stats!

So I wanted to run Jekyll locally on my Fedora 25 install. To do so first requires installing some packages:
```
$ sudo dnf install ruby-devel  
$ sudo dnf install redhat-rpm-config
$ sudo gem install jekyll
```

I had already cloned the repository, but wanted to create a new branch, just in case this all went wrong:
```
$ git checkout -b git run_jekyll_locally
```
This created a new branch called 'run_jekyll_locally', and that can be confirmed using the 'git status' command:
```
$ git status
On branch run_jekyll_locally
nothing to commit, working tree clean
```

Now that I have a clean branch, it's time to run Jekyll locally to serve the site directly on my laptop, firsty run 'jekyll build':
```
$ jekyll build
Configuration file: /home/martyn/Documents/Devel/molo76.github.io/_config.yml
            Source: /home/martyn/Documents/Devel/molo76.github.io
       Destination: /home/martyn/Documents/Devel/molo76.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.374 seconds.
```
And now to serve the site with 'jekyll serve':
```
$ jekyll serve
Configuration file: /home/martyn/Documents/Devel/molo76.github.io/_config.yml
Configuration file: /home/martyn/Documents/Devel/molo76.github.io/_config.yml
            Source: /home/martyn/Documents/Devel/molo76.github.io
       Destination: /home/martyn/Documents/Devel/molo76.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.044 seconds.
 Auto-regeneration: enabled for '/home/martyn/Documents/Devel/molo76.github.io'
Configuration file: /home/martyn/Documents/Devel/molo76.github.io/_config.yml
    Server address: http://127.0.0.1:4000/
```
It worked! Great, so I now created this blog page, and saved it. Checked out http://localhost:4000/blog/ and there it is. I'm now editing the site on a seperate local version.
