---
layout: post
title: "Run Jekyll locally, and a load of git"
date: 2017-05-01
---
Rather than editing this site directly on github through the web front end, I have been using command-line git to clone the repository to my laptop, edit files, then commit and push back to github. It works well but every small edit requires a push into the repository to see the results, good or bad. It becomes a bit time consuming, but does up your github commit stats!

I wanted to run Jekyll locally on my Fedora 25 install, so I can make changes to the website and check they work first, before pushing to the 'master' repository on github. To do this requires installing Jekyll and some dependencies:
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

Checking 'git status' again shows that I have edited a couple of files (correcting typo's errors) that are already in the repository and also created a new file, this blog post:
```
$ git status
On branch run_jekyll_locally
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   about/index.html
	modified:   index.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	_posts/2017-05-01-run-jekyll-locally.md
```
I now run 'git add' on those files to stage them ready for commit, and checking the 'git status' again confirms the changes will be commited:
```
$ git add about/index.html
$ git add index.html
$ git add _posts/2017-05-01-run-jekyll-locally.md
$ git status
On branch run_jekyll_locally
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   _posts/2017-05-01-run-jekyll-locally.md
	modified:   about/index.html
	modified:   index.html
```
Now to commit them:
```
$ git commit -m "altered index.html, about page, added blog post"
[run_jekyll_locally f05b681] altered index.html, about page, added blog post
 3 files changed, 52 insertions(+), 2 deletions(-)
 create mode 100644 _posts/2017-05-01-run-jekyll-locally.md
```
Finally, push the changes that have been committed locally to github:
```
$ git push origin run_jekyll_locally
Counting objects: 11, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (10/10), done.
Writing objects: 100% (11/11), 2.00 KiB | 0 bytes/s, done.
Total 11 (delta 6), reused 0 (delta 0)
remote: Resolving deltas: 100% (6/6), completed with 3 local objects.
To github.com:molo76/molo76.github.io.git
 * [new branch]      run_jekyll_locally -> run_jekyll_locally
```
This creates a new branch on github itself (earlier I just created the branch locally). Looking at the repository on the github website shows the branch. Finally when all is done it's time to merge the branch into the 'master' repository, so the changes will be served on the site on github-pages.

To do this, checkout the 'master' branch, and merge the 'run_jekyll_locally' branch:
```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean

$ git merge run_jekyll_locally
Updating 49f9a9b..80cb1d3
Fast-forward
 _posts/2017-05-01-run-jekyll-locally.md | 81 +++++++++++++++++++++++++++++++++++++++++++++++++++
 about/index.html                        |  2 +-
 index.html                              |  2 +-
 3 files changed, 83 insertions(+), 2 deletions(-)
 create mode 100644 _posts/2017-05-01-run-jekyll-locally.md
```
After checking the status one last time a final push will send all the changes made up to the 'master' branch.

```
[martyn@dubtower molo76.github.io]$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean

$ git push
Total 0 (delta 0), reused 0 (delta 0)
To github.com:molo76/molo76.github.io.git
   49f9a9b..80cb1d3  master -> master
```
At first I thought this had failed, as the push command showed `Total 0 (delta 0), reused 0 (delta 0)`. But the site had updated, meaning the merge worked and final push worked.

To recap my steps in this blog post, I did the following:
* Installed Jekyll locally
* Created a branch of the 'master' repository locally on my laptop
* Started Jekyll to 'build' and 'serve' the site locally
* Added a new blog post
* Commited changes, and pushed new branch to github
* Merged the branch into the 'master' repository
* Pushed the master back to github

That's alot of stuff, and github can be complicated for a newbie such as myself, having no previous knowledge of version control systems. I'm going to go through this process a few more times to let it sink in properly!

A thank you to [dont-be-afraid-to-commit](http://dont-be-afraid-to-commit.readthedocs.io/en/latest/git/commandlinegit.html) which has a good one page starter guide for github on the command line.
