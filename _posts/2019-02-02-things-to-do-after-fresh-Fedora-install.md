---
layout: post
title: "Things to do after a fresh Fedora install"
date: 2019-02-02
---
Look at that! A massive gap in posts, last one being Sept 2017. I could claim to have been too busy, I could admit to being lazy and ignoring this blog thing. Truth is both, I got a new job in Sept 2017, and have been super busy since. I did write a load of posts, but didn't finish any of them in a good enough state to publish. Anyway, here's the first for 2019. 

A task at work required me to install a Linux VM on my MacBook Pro. I haven't installed a fresh Fedora for a while, apart from Vagrant box cli instances. As much as I like Mac OS for work, I really like Fedora with Gnome3 (many, many don't!). As always, there is a bunch of stuff I need to do to get the install just how I want it. I thought I would note them here, so I don't have to search around again next time.

Step 1 - dnf update, of course!

```
sudo dnf update -y
```

Step 2 - Install rpm-fusion repos:

```
dnf install --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-29.noarch.rpm
dnf install --nogpgcheck http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-29.noarch.rpm
```

Step 3 - Install Vivaldi browser:

Download from [here](https://vivaldi.com/download/), then:
```
dnf install -y vivaldi-stable-2.2.1388.37-1.x86_64.rpm
```

Step 4 - Install MultiMedia plugins and VLC player:
```
sudo dnf install gstreamer1-plugins-base gstreamer1-plugins-good gstreamer1-plugins-ugly gstreamer1-plugins-bad-free gstreamer1-plugins-bad-free gstreamer1-plugins-bad-freeworld gstreamer1-plugins-bad-free-extras ffmpeg vlc
```

Step 5 - Install Gnome tweak tool to get min/max window buttons, seriously that still are not in by default! 
```
dnf install gnome-tweak-tool
```

Step 6 - Nearly forgot this one, set hostname to something more interesting:
```
hostnamectl set-hostname --static feds29
```

Step 7 - Install nice pomodoro timer shell extension:
```
sudo dnf install gnome-shell-extension-pomodoro
```

Step 8 - Install Open Weather shell extension: 
```
sudo dnf install gnome-shell-extension-openweather
```
