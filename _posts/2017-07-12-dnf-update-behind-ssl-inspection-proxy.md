---
layout: post
title: "Redhat / CentOS / Fedora dnf update from behind SSL inspection proxy"
date: 2017-07-04
---
I am doing some testing with cloud based secure web access gateway solutions, and while testing with SSL inspection turned on I noticed that from a Fedora box behind the Zscaler cloud I could no longer do a 'dnf update'. The Curl error (60) below is the fatal error, mentioning 'Peers Certificate issue is not recognized'.

```
Install   8 Packages
Upgrade  85 Packages
Remove    5 Packages

Total download size: 303 M
Is this ok [y/N]: y
Downloading Packages:

The downloaded packages were saved in cache until the next successful transaction.
You can remove cached packages by executing 'dnf clean packages'.
Error: Error downloading packages:
  Curl error (60): Peer certificate cannot be authenticated with given CA certificates for https://mirrors.rpmfusion.org/metalink?repo=free-fedora-updates-released-25&arch=x86_64 [Peer's Certificate issuer is not recognized.]
```

So there's something I didn't know, dnf uses curl. There are curl arguments you can use to allow the use of unrecognized certificates, but that is not going help dnf. I looked at dnf arguments but thought that there must be a more permanent solution. 

The point of SSL inspection, done by a proxy or firewall, is that it is essentially a 'man in the middle' interception of data.  The proxy or firewall in the middle of the data flow presents its own certificate to the client during the intial ssl setup, rather than the certificate of the destination website or service. The device in the middle then decrypts traffic from the destination website, inspects it, then re-encrypts it and sends it to the client. 

For this to work transparently to end users, the certificate from the 'device in the middle' needs to be installed as a trusted certificate on the client device, otherewise the browser will flag that the certificate presented does not match the intended destination sites credentials. I had already installed the proxies certificate as a trusted certificate in my Fedora build by using [Kleopatra](https://www.kde.org/applications/utilities/kleopatra/), however dnf was still giving me the curl error 60 issue. 

I found a quick hack which suggested that adding the line ```sslverify=0``` to ```/etc/dnf/dnf.conf``` will fix the issue. From a security point of view that doesn't sit well with me, as it essentially means that dnf will accept any certificate from any source. The better solution is to add the proxies certificate, in PEM format, to the ```/etc/pki/ca-trust/source/anchors/``` folder and then run the ```sudo update-ca-trust```. 

And there we go, dnf now works through an upstream device that is doing ssl inspection. The same probably applies to the older yum update process, and it looks like I'll need to check with apt based distributions to test that out too, since alot of our dev users are Ubuntu based. 

