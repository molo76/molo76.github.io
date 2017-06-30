---
layout: post
title: "Create a large file for testing on linux"
date: 2017-06-30
---

I wanted to do some testing of a cloud based next-gen firewall at work, and ideally I wanted to run a bunch of SSH/SCP file transfers to generate some traffic and log data. 

Linux has the 'dd' command (Data Duplicator), which I have used in the past, but it is quite slow to create a large file:
```
dd if=/dev/zero of=./testfile.img bs=4k iflag=fullblock,count_bytes count=10G
```

I found the following 'fallocate' command, and it's super quick to create a large file, much faster than 'dd'. Fallocate is described as 'Preallocate or deallocate space to a file'. 
```
fallocate -l 10G gentoo_root.img
```

Thank you StackOverflow my friend, I found this nugget <a href='https://stackoverflow.com/questions/257844/quickly-create-a-large-file-on-a-linux-system'>here</a>.
