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


/etc/pki/ca-trust/source/anchors/

update-ca-trust 

edit /etc/dnf/dnf.conf and add sslverify=0

