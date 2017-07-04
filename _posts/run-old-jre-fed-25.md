---
layout: post
title: "Run an old JRE on Fedora 25"
date: 2017-07-04
---
Back in 2013 I did a firewall migration & LAN upgrade project for a site I worked at. I pretty much did the whole thing myself and found that I needed some sort of 'project software' to help me. I found this great app called <a href='https://sourceforge.net/projects/thinkingrock/?source=navbar'>Thinking Rock</a> and it really helped me get my tasks and project in order. The bonus that being a java app it runs on Linux too. 

Now I'm back doing some project work I looked for it again. There is a new version, <a href='https://www.trgtd.com.au/'>3.1</a>, that has some nice bells and whistles, but it's $39. I found version 2.2.1 hosted on <a href='https://sourceforge.net/projects/thinkingrock/?source=navbar'>SourceForge</a> did everything I needed, so I went and grabbed it again. 

It failed to run on Fedora 25, no error, just splash screen then nothing. Then I found that it requires java 1.6, and will not run with newer versions (fed 25 ships with java 1.8). So I installed java 1.6 alongside the 1.8 that Fedora 25 ships: 

```
sudo dnf install java-1.6.0-openjdk --releasever=16 --nogpgcheck
```

Then I edited the ```ThinkingRock/tr-2.2.1/etc/tr.conf``` file, adding in the jdkhome location of java 1.6

```
### Default location of Java JDK/JRE, can be overridden by using --jdkhome <dir> switch ###
jdkhome="/usr/lib/jvm/jre-1.6.0-openjdk.x86_64"
```

And now Thinking Rock runs! I put this post up, as I have several Fedora installs I may want to run it on, so will probably visit this page again myself soon. :) 
