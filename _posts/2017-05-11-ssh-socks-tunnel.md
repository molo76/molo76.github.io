---
layout: post
title: "http access through socks-ssh-tunnel"
date: 2017-05-11
---
To browse the internet via an AWS server, of any other remote server running ssh, run the following command: 

```
ssh -D 8123 -f -C -q -N user@ssh-server-ip
```
Of course, the target server has to be able to access the internet. The command arguments used above are: 
  *```-D```: Tells SSH that we want a SOCKS tunnel on the specified port number (you can choose a number between 1025-65536)
  *```-f```: Forks the process to the background
  *```-C```: Compresses the data before sending it
  *```-q```: Uses quiet mode
  *```-N```: Tells SSH that no command will be sent once the tunnel is up

Then set the browser of choice to use socks proxy ```localhost 8123``` and go browse. It works well if you use a server in another country (aws / digital ocean etc) to get round some geo-ip content restrictions. Be mindful to consider if you are charged bandwidth by that remote server service, and the effect of using it for general browsing / streaming. 

