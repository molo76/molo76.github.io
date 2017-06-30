---
layout: post
title: "Throwing some IPs around in Python Part I"
date: 2017-06-06
---
I started to mess around with some IP addresses in Python, and I wanted to create a simple subnet-calculator where the user enters an IP and CIDR mask, '10.208.20.1/25' and the program outputs the following information: 
* Network address: 10.208.20.0
* Broadcast address: 255.255.255.128
* Subnet mask: 255.255.255.128
* First host ip: 10.208.20.1
* Last host ip: 10.208.20.126
* Number of host ips available: 126

Here is what I have so far......

First of all, get some user input, and cut it up into an 'ip' and a 'mask' variable 

```
# get the user to enter an IP/mask and add it to variable y
>>> y = input('Enter an IP address & mask, example 10.100.23.1/23: ')
Enter an IP address & mask, example 10.100.23.1/23: 200.54.23.1/24
>>> 
>>> y
'200.54.23.1/24'

# Split the y variable on the '/' character
>>> ip,mask = y.split('/')
>>> 
>>> ip
'200.54.23.1'
>>> 
>>> mask
'24'
>>> 
```

So now we have the two parts of the network, in two seperate variable. Next up is splitting into octets, then doing some binary conversions to get the info we need. 
