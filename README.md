# aur-eclipse-che-arm
Eclipse Che package build for Archlinux ARM
using instructions found here:
https://blog.benjamin-cabe.com/2016/04/01/running-eclipse-che-on-a-raspberry-pi

This is work in progress.

During installation a user "eclipse-che" with uid and gid 1000 is created.
Eclipse che is installed in /usr/share/eclipse-che
Some (but not yet all) userdata go to /var/lib/eclipse-che.

IP-Address and Port can be configured on /etc/conf.d/eclipse-che