# aur-eclipse-che-arm
Eclipse Che package build for Archlinux ARM
using instructions found here:

https://blog.benjamin-cabe.com/2016/04/01/running-eclipse-che-on-a-raspberry-pi

This is work in progress.

* During installation a user "eclipse-che" with uid and gid 1000 is created.
* Eclipse che is installed in /usr/share/eclipse-che
* Some (but not yet all) userdata go to /var/lib/eclipse-che.

IP-Address and Port can be configured in /etc/conf.d/eclipse-che

As previous versions did not work with current Archlinux systems, this build uses a SNAPSHOT build directly from Jenkins. Therefor it will be necessary to change the download link in the PKGBUILD to a currently available version.

For more information have a look here:

https://github.com/eclipse/che/issues/745

https://github.com/eclipse/che/pull/1550