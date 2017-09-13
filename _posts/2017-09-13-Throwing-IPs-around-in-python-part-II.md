---
layout: post
title: "Throwing some IPs around in Python Part II"
date: 2017-09-13
---
Continuing on from [Throwing IPs around in python part I](https://molo76.github.io/2017/06/06/Throwing-IPs-around-in-python-part-I.html), I had gotten to the point where I had user input, in the format of 'IP/[CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) mask', such as '192.168.10.1/25' and then split that into two variables: 

```
>>> ip
'192.168.10.1'
>>> 
>>> mask
'25'
```
Straight away I have the IP and CIDR mask. IPs are really 32 bit binary numbers. The format we commonly use for IPs is the 'dotted decimal' format, 192.168.10.1 for example. In dotted decimal format each octet (8 bits) is converted to decimal to make the IP easy to read. Working with 192.168.10.1 is much easier than working with the binary version 11000000101010000000101001100001! 

But to work out the details I want from the IP/CIDR input, such as broadcast address & number of host IPs, I need to work with the IP in it's binary format. I need each octet of the dotted decimal notation in binary, and the whole IP as binary string. 

To do that I first split the IP into a list, containing 4 elements, each section of the IP:
```
>>> octets = ip.split('.')
```
Resulting list:
```
>>> octets
['192', '168', '10', '97']
```
Then I looped through the list and converted each of the four strings into binary. Before doing that I had to create an empty list to append each binary octet to: 
```
>>> binary_octets = []
>>> for octet in octets:
...     binary_octets.append(int(bin(int(octet))[2:]))
```
Resulting list:
```
>>> binary_octets
[11000000, 10101000, 1010, 1100001]
```
Now we have each octet in decimal format too. The interesting part of the above is the append function, within the loop ```binary_octets.append(int(bin(int(octet))[2:]))```
